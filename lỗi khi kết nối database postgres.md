```# PostgreSQL Configuration

POSTGRES_IMAGE=postgres:15

POSTGRES_USER=evisor

POSTGRES_PASSWORD=Ev1s0r2025

POSTGRES_DB=estecdb

POSTGRES_HOST=postgres

POSTGRES_PORT_INTERNAL=5432

POSTGRES_PORT_EXTERNAL=5432
```


![[lỗi khi kết nối database postgres.png]]

Chào bạn, lỗi này xảy ra do bạn đang nhầm lẫn giữa cách các dịch vụ "nói chuyện" với nhau **bên trong Docker** và cách bạn kết nối từ **máy tính của mình vào Docker**.

Cấu hình của bạn trong DBeaver đang bị sai ở mục **`Host`**.

---

### ## Giải thích Vấn đề

- **`POSTGRES_HOST=postgres`:** Giá trị `postgres` này là **tên dịch vụ** bên trong mạng ảo của Docker. Chỉ có các container khác trong cùng mạng đó (như container `backend`) mới có thể dùng tên này để kết nối đến database. Nó giống như một "biệt danh" chỉ có người trong nhà mới hiểu.
    
- **DBeaver (trên máy của bạn):** DBeaver là một ứng dụng chạy bên ngoài môi trường Docker. Nó không hiểu "biệt danh" `postgres` là gì. Để kết nối vào container PostgreSQL từ máy tính của bạn, bạn phải dùng địa chỉ mà Docker đã "mở ra" cho máy tính của bạn, đó chính là **`localhost`** (hoặc `127.0.0.1`).
    

Lỗi "The connection attempt failed" xảy ra vì DBeaver đang cố gắng tìm một máy chủ tên là `postgres` trên mạng của bạn và không tìm thấy.

---

### ## Cách khắc phục 🛠️

Trong cửa sổ "Connection Settings" của DBeaver, bạn chỉ cần sửa lại một mục duy nhất:

1. Tìm đến trường **`Host`**.
    
2. Thay đổi giá trị hiện tại thành **`localhost`**.
    

Mọi thông tin khác như `Port` (5432), `Database` (estecdb), `Username` (evisor), và `Password` (Ev1s0r2025) của bạn đã đúng.

Sau khi sửa lại `Host` thành `localhost` và nhấn **Test Connection**, kết nối sẽ thành công. ✅


---
---

![[lỗi khi kết nối database postgres-1.png]]

![[lỗi khi kết nối database postgres-2.png]]

Rất tiếc, mặc dù bạn đã nhập đúng mật khẩu đang có, lỗi này vẫn xảy ra. Đây là lỗi **xác thực mật khẩu thất bại** và nó có nghĩa là mật khẩu bạn nhập trong DBeaver **không khớp** với mật khẩu mà database PostgreSQL hiện đang sử dụng.

Nguyên nhân rất có thể là do **dữ liệu cũ của database vẫn còn tồn tại** từ những lần chạy Docker trước đó với một mật khẩu sai.

---

### ## Giải thích Vấn đề

Khi bạn chạy `docker-compose up` lần đầu tiên, Docker sẽ tạo ra một vùng lưu trữ riêng (volume) để giữ lại dữ liệu cho PostgreSQL, bao gồm cả mật khẩu của user `evisor` lúc đó.

Nếu sau này bạn sửa mật khẩu trong file `.env` hoặc `docker-compose.yaml` và chỉ chạy lại `docker-compose up`, Docker sẽ không tạo lại database từ đầu mà vẫn dùng lại dữ liệu cũ với mật khẩu cũ. Vì vậy, dù bạn đã sửa mật khẩu trong file cấu hình, database vẫn đang dùng mật khẩu sai từ lần khởi tạo đầu tiên.

---

### ## Cách khắc phục triệt để 🛠️

Để buộc Docker tạo lại database một cách "sạch sẽ" với đúng mật khẩu mới nhất, bạn cần **xóa hoàn toàn môi trường cũ** đi.

1. **Dọn dẹp môi trường cũ:**
    
    - Mở terminal trong thư mục dự án backend.
        
    - Chạy lệnh sau để dừng, xóa các container và **xóa cả volume chứa dữ liệu cũ của database**:
        
        Bash
        
        ```
        docker-compose down -v
        ```
        
    
    _(Tùy chọn `-v` là để xóa volumes, đây là bước quan trọng nhất)_
    
2. **Khởi động lại từ đầu:**
    
    - Sau khi dọn dẹp xong, hãy chạy lại lệnh để Docker dựng lại toàn bộ hệ thống. Nó sẽ đọc mật khẩu chính xác từ file cấu hình của bạn và tạo database mới.
        
        Bash
        
        ```
        docker-compose up -d
        ```
        
3. **Thử lại kết nối:**
    
    - Đợi khoảng 15-20 giây để database có thời gian khởi tạo.
        
    - Bây giờ, hãy quay lại DBeaver và nhấn nút **Test Connection**. Lần này kết nối sẽ thành công.

---
---

```
FATAL: no pg_hba.conf entry for host "192.168.54.152", user "evisor", database "estecdb", no encryption

FATAL: no pg_hba.conf entry for host "192.168.54.152", user "evisor", database "estecdb", no encryption
```

Lỗi này có nghĩa là **database PostgreSQL đang từ chối kết nối** từ máy tính của bạn vì nó không được cấu hình để "tin tưởng" địa chỉ IP `192.168.54.152`.

Đây là một lỗi về cấu hình phía server database, không phải lỗi sai mật khẩu.

### ## Giải thích Vấn đề

Hãy tưởng tượng database PostgreSQL của bạn là một club và file `pg_hba.conf` là danh sách khách mời của người bảo vệ.

- Bạn (từ IP `192.168.54.152`) đang cố gắng vào club.
    
- Người bảo vệ (PostgreSQL) kiểm tra danh sách (`pg_hba.conf`) và thấy rằng địa chỉ của bạn không có trong đó, vì vậy họ từ chối cho bạn vào.
    

Lỗi này thường xảy ra với ảnh Docker `postgres:15` mặc định, nó chỉ cho phép kết nối từ bên trong mạng Docker (`localhost` của container) chứ không cho phép kết nối từ máy chủ bên ngoài.

---

### ## Cách khắc phục 🛠️

Bạn cần "bảo" PostgreSQL rằng hãy tin tưởng và chấp nhận các kết nối từ bất kỳ địa chỉ IP nào. Cách dễ nhất để làm điều này là thêm một biến môi trường vào file `docker-compose.yaml`.

1. **Mở file `docker-compose.yaml`** trong thư mục dự án backend.
    
2. Tìm đến phần dịch vụ `postgres`.
    
3. Thêm dòng sau vào dưới mục `environment`:
    
    YAML
    
    ```
    POSTGRES_HOST_AUTH_METHOD: trust
    ```
    
    Phần cấu hình `postgres` của bạn sẽ trông như thế này:
    
    YAML
    
    ```
    # File: docker-compose.yaml
    
    services:
      postgres:
        image: postgres:15
        environment:
          POSTGRES_USER: ${POSTGRES_USER}
          POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
          POSTGRES_DB: ${POSTGRES_DB}
          POSTGRES_HOST_AUTH_METHOD: trust # <--- THÊM DÒNG NÀY
        ports:
          - "${POSTGRES_PORT_EXTERNAL}:${POSTGRES_PORT_INTERNAL}"
        # ... các cấu hình khác
    ```
    
    **Lưu ý:** `trust` có nghĩa là chấp nhận mọi kết nối mà không cần mật khẩu. Điều này ổn cho môi trường phát triển (development) nhưng **không an toàn** cho môi trường production.
    
4. **Dọn dẹp và khởi động lại Docker:** Để thay đổi này có hiệu lực, bạn cần tạo lại container database.
    
    Bash
    
    ```
    # Dừng và xóa môi trường cũ
    docker-compose down -v
    
    # Khởi động lại với cấu hình mới
    docker-compose up -d
    ```
    
5. **Thử lại kết nối:** Đợi khoảng 15-20 giây, sau đó quay lại DBeaver và **Test Connection**. Lần này kết nối sẽ thành công.