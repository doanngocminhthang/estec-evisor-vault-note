Chào bạn,

Đây là một nhiệm vụ quản lý hệ thống rất quan trọng để đảm bảo an ninh và vận hành ổn định. Để thực hiện, bạn cần kết hợp hai việc: **tạo một cấu trúc file Excel hợp lý** và **sử dụng các công cụ để rà soát** các port đang được sử dụng.

Dưới đây là một mẫu và quy trình chi tiết.

---

### ## 1. Tạo Cấu trúc File Excel (Mẫu Gợi ý)

Bạn nên tạo một file Excel với các cột sau để theo dõi. Đây là những thông tin quan trọng nhất.

|Số Port|Giao thức (TCP/UDP)|Tên Dịch vụ/Ứng dụng|Dự án|Mục đích Sử dụng|Trạng thái (Mở/Đóng)|Ghi chú|
|---|---|---|---|---|---|---|
|**8000**|TCP|Django Dev Server|WildFire-Web|Chạy server web Django để phát triển|Mở (Local)|Chỉ dùng cho team dev|
|**15432**|TCP|PostgreSQL|WildFire-Web|Cơ sở dữ liệu chính cho dự án|Mở (Nội bộ)|Chỉ cho phép server web kết nối|
|**22**|TCP|SSH|Quản trị Server|Đăng nhập và quản trị server từ xa|Mở (Hạn chế IP)|Chỉ mở cho IP văn phòng|
|**80**|TCP|Nginx / Web Server|WildFire-Web|Cổng HTTP công khai cho người dùng|Mở (Công khai)||
|**443**|TCP|Nginx / Web Server|WildFire-Web|Cổng HTTPS (bảo mật) công khai|Mở (Công khai)||
|**5632**|TCP|Django (Gunicorn)|WildFire-Web|Cổng ứng dụng Django chạy production|Mở (Nội bộ)|Nginx sẽ trỏ vào cổng này|

Xuất sang Trang tính

---

### ## 2. Cách Tìm kiếm và Thu thập Thông tin

Bây giờ, làm sao để điền thông tin vào bảng này? Bạn cần làm một người "thám tử" hệ thống.

#### **A. Rà soát trực tiếp trên Server**

Đăng nhập vào máy chủ của bạn và dùng các lệnh sau để xem các port đang "lắng nghe" (LISTENING).

- **Trên Linux:**
    
    Bash
    
    ```
    # Lệnh này hiển thị tất cả các port TCP và UDP đang lắng nghe,
    # cùng với tên tiến trình đang sử dụng chúng.
    sudo ss -tulnp
    ```
    
    _hoặc lệnh cũ hơn:_
    
    Bash
    
    ```
    sudo netstat -tulnp
    ```
    
- **Trên Windows (dùng PowerShell):**
    
    PowerShell
    
    ```
    # Lấy các kết nối TCP đang lắng nghe
    Get-NetTCPConnection -State Listen
    ```
    
    _hoặc dùng Command Prompt:_
    
    DOS
    
    ```
    netstat -ano | findstr "LISTENING"
    ```
    

#### **B. Kiểm tra từ File Cấu hình (Cách tốt nhất)**

Đây là cách chính xác nhất để biết một dự án được _thiết kế_ để chạy trên port nào.

- **Docker:** Mở file `docker-compose.yaml` và tìm đến phần `ports`.
    
    YAML
    
    ```
    services:
      postgres:
        image: postgres:latest
        ports:
          - "15432:5432" # <-- Port 15432 đang được sử dụng
    ```
    
- **Mã nguồn Ứng dụng:** Tìm trong code của dự án xem nó được cấu hình chạy ở port nào (ví dụ: `manage.py runserver 0.0.0.0:8000`).
    
- **Cấu hình Web Server (Nginx, Apache):** Mở các file cấu hình (`.conf`) để xem chúng đang lắng nghe ở cổng 80, 443 và đang trỏ vào các cổng ứng dụng nào.
    

#### **C. Dùng Công cụ Quét Port**

Bạn có thể dùng công cụ như `nmap` để quét từ một máy tính khác trong cùng mạng để xem server đang mở những port nào.

Bash

```
# Quét 1000 port phổ biến nhất trên server
nmap <địa_chỉ_IP_server>

# Quét tất cả 65535 port
nmap -p 1-65535 <địa_chỉ_IP_server>
```

---

### ## 3. Một số Port Phổ biến để Tham khảo

- **22:** SSH (Đăng nhập vào server Linux)
    
- **80:** HTTP (Web không bảo mật)
    
- **443:** HTTPS (Web có bảo mật)
    
- **5432:** PostgreSQL
    
- **3306:** MySQL / MariaDB
    
- **3389:** Remote Desktop (Điều khiển máy tính Windows từ xa)
    
- **8000, 8080:** Các cổng phổ biến cho server web phát triển
    

**Lời khuyên:** Đây không phải là công việc làm một lần. Hãy lưu file Excel này ở một nơi chung và cập nhật nó mỗi khi có sự thay đổi về cấu hình hệ thống.