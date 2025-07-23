Chắc chắn rồi! "Truy vấn database" nghe có vẻ phức tạp, nhưng thực chất nó giống hệt như cách bạn tìm sách trong một thư viện khổng lồ.

Hãy dùng chính code trong file Authentication.py của bạn để giải thích quy trình này một cách chi tiết và dễ hiểu nhất.

---

### **Analogy: Database như một Thư viện**

- **Database (postgres):** Là cả thư viện.
    
- **Bảng (Table, ví dụ: User, Session):** Là các kệ sách chuyên đề (Kệ sách "Người dùng", Kệ sách "Phiên đăng nhập").
    
- **Dòng (Row):** Là một cuốn sách cụ thể trên kệ.
    
- **Cột (Column, ví dụ: username, password):** Là các thông tin trên bìa sách (Tên sách, Tác giả).
    
- **Code Python của bạn:** Là bạn, người đi tìm sách.
    
- **conn (Connection):** Là chiếc thẻ thư viện, cho phép bạn vào bên trong.
    
- **cursor (Cursor):** Là người thủ thư. Bạn không tự chạy lung tung đi tìm sách, bạn đưa yêu cầu cho người thủ thư, và họ sẽ đi tìm giúp bạn.
    
- **Câu lệnh SQL (query):** Là "phiếu yêu cầu" bạn điền thông tin để đưa cho người thủ thư.
    
![[Giải thích truy vấn database như thế nào.png]]


---

### **Bước 1: "Vào thư viện" - Mở kết nối (conn)**

Trước khi làm bất cứ điều gì, code của bạn phải "mở cửa" và "bước vào" thư viện. Đây chính là hàm get_postgres_connection() mà chúng ta đã phân tích. Nó tạo ra đối tượng conn.

### **Bước 2: "Đến quầy thủ thư" - Tạo một Cursor**

Khi đã vào thư viện, bạn đến quầy và nói "Tôi muốn bắt đầu một giao dịch".

Generated python

```
cursor = conn.cursor()
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

Lệnh này tạo ra một cursor (người thủ thư) sẵn sàng nhận các yêu cầu (câu lệnh SQL) của bạn.

---

### **Bước 3: "Viết phiếu yêu cầu" - Câu lệnh SQL**

Đây là phần cốt lõi. Bạn viết ra chính xác điều bạn muốn.

#### **Ví dụ 1: Truy vấn TÌM KIẾM (SELECT)**

Trong hàm Authentication_function:

Generated python

```
query = """
    SELECT "username", "password", "avatar", "full_name" 
    FROM "User" 
    WHERE "username" = %s AND "password" = %s
"""
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

Hãy đọc câu này như đọc tiếng Việt:

- **SELECT "username", "password", ...**: "LẤY CHO TÔI thông tin từ các cột username, password, avatar, full_name..."
    
- **FROM "User"**: "...từ kệ sách tên là User..."
    
- **WHERE "username" = %s AND "password" = %s**: "...VỚI ĐIỀU KIỆN là cột username phải bằng giá trị thứ nhất tôi cung cấp, VÀ cột password phải bằng giá trị thứ hai tôi cung cấp."
    

**%s là gì?**  
Đây là một "chỗ giữ chỗ" cực kỳ quan trọng để **chống lại một kiểu tấn công tên là SQL Injection**. Thay vì tự mình ghép chuỗi (ví dụ f"...WHERE username = '{input.username}'"), bạn đưa câu lệnh và dữ liệu một cách riêng biệt. Thư viện database sẽ tự động "làm sạch" và điền dữ liệu vào chỗ %s một cách an toàn.

---

### **Bước 4: "Đưa phiếu cho thủ thư" - Thực thi câu lệnh (execute)**

Bây giờ bạn đưa cái phiếu yêu cầu đó cho người thủ thư.

Generated python

```
cursor.execute(query, (input.username, input.password))
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

- **Hành động:** cursor sẽ cầm câu query và cặp dữ liệu (input.username, input.password) gửi đến database. Database sẽ điền dữ liệu vào các chỗ %s một cách an toàn và chạy lệnh tìm kiếm.
    

---

### **Bước 5: "Nhận sách" - Lấy kết quả (fetch)**

Sau khi thủ thư tìm xong, họ sẽ đưa sách cho bạn.

Generated python

```
user = cursor.fetchone()
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

- **fetchone()**: Lấy **một** cuốn sách (một dòng) đầu tiên mà thủ thư tìm thấy.
    
- **Nếu tìm thấy:** user sẽ là một tuple chứa các giá trị bạn yêu cầu, ví dụ ('hoanvlh', 'Ef27Xw34', 'avatar.png', 'Vo Ly Hoang Hoan').
    
- **Nếu không tìm thấy:** user sẽ là None. Đây chính là cách code của bạn biết được đăng nhập thất bại.
    

---

### **Bước 6: Truy vấn THAY ĐỔI DỮ LIỆU (INSERT, UPDATE, DELETE)**

Đối với các hành động làm thay đổi dữ liệu (thêm sách, sửa bìa sách, vứt sách đi), quy trình tương tự nhưng có thêm một bước cực kỳ quan trọng.

**Ví dụ: INSERT (Thêm phiên đăng nhập mới)**

Generated python

```
insert_query = """
    INSERT INTO "Session" ("session_id", "user_id", "created_at", "expires_at")
    VALUES (%s, %s, %s, %s)
"""
cursor.execute(insert_query, (session_id, user[0], created_at, expires_at))
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

- **Đọc là:** "THÊM VÀO kệ sách Session, vào các cột session_id, user_id... các GIÁ TRỊ tương ứng là ...".
    

**Bước 6.5: "ĐÓNG DẤU XÁC NHẬN" - commit()**

Generated python

```
conn.commit()
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

- **Đây là bước quan trọng nhất khi thay đổi dữ liệu.** Hãy tưởng tượng sau khi bạn yêu cầu thủ thư thêm một cuốn sách mới, bạn phải ký vào sổ và đóng dấu "Xác nhận". Nếu không có bước này, mọi thay đổi (INSERT, UPDATE, DELETE) của bạn sẽ chỉ là tạm thời và sẽ bị hủy bỏ khi giao dịch kết thúc.
    
- **Góc nhìn của Tester:** Nếu một chức năng "dường như" hoạt động nhưng dữ liệu không thực sự thay đổi trong database, rất có thể lập trình viên đã **quên conn.commit()**.
    

---

### **Bước 7: "Chào thủ thư và ra về" - Đóng kết nối (close)**

Generated python

```
finally:
    cursor.close()
    conn.close()
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

- **cursor.close()**: "Tôi xong việc với anh thủ thư này rồi."
    
- **conn.close()**: "Tôi ra khỏi thư viện đây." (Đóng thẻ thư viện).
    
- **Tại sao lại quan trọng?** Mỗi kết nối đến database đều chiếm một lượng tài nguyên. Nếu bạn mở kết nối mà không đóng, sau một thời gian server sẽ hết tài nguyên và bị treo. Đặt chúng trong finally đảm bảo chúng luôn được thực thi.
    

**Tóm lại, quy trình truy vấn database trong code của bạn là một chu trình an toàn và chuẩn mực: Lấy địa chỉ -> Mở kết nối -> Nhờ "thủ thư" thực hiện yêu cầu -> Nhận kết quả -> Đóng dấu xác nhận nếu có thay đổi -> Đóng kết nối.**