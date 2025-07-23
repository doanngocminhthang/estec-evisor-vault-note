Chắc chắn rồi! Hiểu cách ứng dụng kết nối đến database là một trong những kỹ năng quan trọng nhất của tester, vì đây là nơi rất nhiều lỗi có thể xảy ra.

Hãy cùng phân tích chi tiết quy trình kết nối đến database PostgreSQL trong dự án của bạn. Nó diễn ra theo 3 bước chính: **Lấy địa chỉ -> Mở kết nối -> Giao tiếp.**

---

### **Bối cảnh: Tại sao lại cần Database?**

Database (cơ sở dữ liệu) PostgreSQL trong dự án của bạn đóng vai trò là "bộ nhớ dài hạn". Nó lưu trữ những thông tin quan trọng và cần tồn tại lâu dài, ví dụ:

- **Bảng User:** Lưu danh sách người dùng, mật khẩu, tên đầy đủ, avatar...
    
- **Bảng Session:** Lưu các phiên đăng nhập hợp lệ của người dùng.
    
- (Có thể) Các bảng khác để lưu kết quả, lịch sử công việc...
    

Bất cứ khi nào ứng dụng cần đọc hoặc ghi những thông tin này, nó phải thực hiện một kết nối đến database.

---

### **Bước 1: Lấy "Địa chỉ" của Database từ file .env**

Giống như bạn cần địa chỉ để gửi thư, ứng dụng cần "địa chỉ" để kết nối đến database. Địa chỉ này được tạo thành từ 5 thông tin cốt lõi.

Trong file main.py, bạn sẽ thấy đoạn code này:

Generated python

```
# Tải biến môi trường từ file .env
load_dotenv()
POSTGRESQL_SERVER = os.getenv("POSTGRESQL_SERVER")
POSTGRES_PORT_EXTERNAL = os.getenv("POSTGRES_PORT_EXTERNAL")
POSTGRES_DB = os.getenv("POSTGRES_DB")
POSTGRES_USER = os.getenv("POSTGRES_USER")
POSTGRES_PASSWORD = os.getenv("POSTGRES_PASSWORD")
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

- **load_dotenv()**: Lệnh này đọc file .env trong thư mục dự án của bạn.
    
- **os.getenv(...)**: Lệnh này lấy giá trị của từng biến từ file .env.
    

**5 thành phần của "địa chỉ":**

1. **POSTGRESQL_SERVER**: Tên máy chủ hoặc địa chỉ IP của database. Khi chạy với Docker, đây thường là tên của service (ví dụ: postgres). Khi chạy trên máy cá nhân, nó có thể là localhost hoặc 127.0.0.1.
    
2. **POSTGRES_PORT_EXTERNAL**: Số "cổng" mà database đang lắng nghe. Giống như số căn hộ trong một tòa nhà. Mặc định của PostgreSQL là 5432.
    
3. **POSTGRES_DB**: Tên của cơ sở dữ liệu cụ thể bạn muốn kết nối vào (một server có thể chứa nhiều database).
    
4. **POSTGRES_USER**: Tên người dùng có quyền truy cập vào database đó.
    
5. **POSTGRES_PASSWORD**: Mật khẩu của người dùng trên.
    

**Góc nhìn của Tester:** Đây là điểm thất bại đầu tiên. Nếu bất kỳ giá trị nào trong file .env bị sai (sai mật khẩu, sai tên database), kết nối sẽ thất bại.

---

### **Bước 2: Thực hiện Kết nối bằng hàm get_postgres_connection**

Trong mỗi hàm API (ví dụ Authentication_api), bạn thấy dòng này:

Generated python

```
conn = get_postgres_connection(POSTGRESQL_SERVER, POSTGRES_PORT_EXTERNAL, POSTGRES_DB, POSTGRES_USER, POSTGRES_PASSWORD)
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

- **Hành động:** Dòng này gọi đến một hàm chuyên dụng (được định nghĩa trong src/DB_Connection.py) và truyền vào 5 thông tin "địa chỉ" đã lấy ở Bước 1.
    
- **Bên trong get_postgres_connection (suy đoán):** Hàm này rất có thể sử dụng một thư viện Python phổ biến tên là psycopg2 để thực hiện kết nối. Nó sẽ trông giống như thế này:
    
    Generated python
    
    ```
    # Bên trong file DB_Connection.py (ví dụ)
    import psycopg2
    
    def get_postgres_connection(host, port, dbname, user, password):
        conn = psycopg2.connect(
            host=host,
            port=port,
            dbname=dbname,
            user=user,
            password=password
        )
        return conn
    ```
    
    Use code [with caution](https://support.google.com/legal/answer/13505487).Python
    
- **Kết quả:** Nếu thành công, biến conn sẽ chứa một **đối tượng kết nối (connection object)**. Hãy tưởng tượng nó như một "đường dây điện thoại" đã được kết nối thành công đến database. Nếu thất bại, nó sẽ gây ra một lỗi (Exception).
    

**Góc nhìn của Tester:** Đây là điểm thất bại thứ hai. Nếu database server không chạy (ví dụ: container Docker bị tắt), hàm psycopg2.connect sẽ thất bại và gây ra lỗi **ConnectionRefusedError**. Đây chính là lỗi bạn đã thấy trước đây!

---

### **Bước 3: Giao tiếp với Database qua Connection và Cursor**

Sau khi đã có "đường dây điện thoại" (conn), bạn cần một "người giao dịch viên" để gửi lệnh và nhận kết quả. Đó chính là **cursor**.

Trong file Authentication.py, bạn thấy các lệnh này:

Generated python

```
# 1. Mở một phiên giao dịch
cursor = conn.cursor()

# 2. Gửi một câu lệnh (query)
query = """SELECT ..."""
cursor.execute(query, (input.username, input.password))

# 3. Nhận kết quả
user = cursor.fetchone()

# 4. Lưu thay đổi (nếu có INSERT, UPDATE, DELETE)
conn.commit()

# 5. Đóng phiên giao dịch và kết nối
cursor.close()
conn.close()
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

- **conn.cursor()**: Tạo ra một đối tượng cursor. Mỗi cursor đại diện cho một phiên làm việc với database.
    
- **cursor.execute(query, ...)**: Gửi một câu lệnh SQL đến database để thực thi.
    
- **cursor.fetchone()**: Đọc **một** dòng kết quả trả về. (Nếu muốn đọc nhiều dòng, ta dùng fetchall()).
    
- **conn.commit()**: **CỰC KỲ QUAN TRỌNG.** Lệnh này có nghĩa là "Lưu vĩnh viễn tất cả các thay đổi (INSERT, UPDATE, DELETE) mà tôi vừa thực hiện". Nếu thiếu lệnh này, mọi thay đổi sẽ bị hủy bỏ khi kết nối đóng lại.
    
- **cursor.close() và conn.close()**: "Cúp máy". Hành động này giải phóng tài nguyên trên cả ứng dụng và database server. Việc đặt chúng trong khối finally là một thực hành rất tốt, đảm bảo kết nối luôn được đóng lại dù có lỗi xảy ra hay không.
    

**Góc nhìn của Tester:**

- **Lỗi logic:** Câu query SQL có thể bị sai.
    
- **Lỗi dữ liệu:** Dữ liệu trong database có thể không như mong đợi (ví dụ: người dùng test không tồn tại).
    
- **Lỗi transaction:** Nếu lập trình viên quên conn.commit(), chức năng đổi mật khẩu có thể báo thành công nhưng thực tế mật khẩu không hề được thay đổi trong DB.
    
- **Lỗi rò rỉ tài nguyên (Resource Leak):** Nếu quên conn.close(), ứng dụng có thể bị treo sau một thời gian hoạt động vì đã mở quá nhiều kết nối mà không đóng chúng lại.