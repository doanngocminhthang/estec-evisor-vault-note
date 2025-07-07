https://app.remote.it/#/devices/90:00:00:00:00:26:00:68/90:00:00:00:00:26:00:69/connect

Mật khẩu cho kết nối ssh : x@X123456789




---

Cách sử dụng 😀

**Xin chúc mừng!**

Thông báo bạn vừa nhận được là **dấu hiệu cho thấy bạn đã kết nối SSH thành công vào `rnd-server`!**

Dòng `rnd@rnd-Default-string:~$` ở cuối cho biết bạn đã đăng nhập với tài khoản `rnd` và hiện đang ở trên terminal của server, sẵn sàng thực hiện các lệnh.

**Giải thích các dòng bạn thấy:**

- **`Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-60-generic x86_64)`**: Đây là thông báo chào mừng từ hệ điều hành Ubuntu đang chạy trên `rnd-server`. Nó cho biết bạn đang ở trên phiên bản Ubuntu 22.04.5 LTS (Long Term Support), chạy nhân Linux phiên bản 6.8.0-60 trên kiến trúc 64-bit.
    
- **`* Documentation: https://help.ubuntu.com`**
    
- **`* Management: https://landscape.canonical.com`**
    
- **`* Support: https://ubuntu.com/pro`**: Đây là các đường dẫn hữu ích để tìm tài liệu, công cụ quản lý và hỗ trợ cho Ubuntu.
    
- **`Expanded Security Maintenance for Applications is not enabled.`**: Thông báo liên quan đến dịch vụ bảo mật mở rộng của Ubuntu, không quan trọng lắm đối với việc sử dụng cơ bản của bạn.
    
- **`6 updates can be applied immediately.`**
    
- **`To see these additional updates run: apt list --upgradable`**: Hệ thống đang báo có 6 gói phần mềm có thể cập nhật ngay lập tức. Nếu bạn muốn xem đó là những gói nào, bạn có thể chạy lệnh `apt list --upgradable`.
    
- **`1 additional security update can be applied with ESM Apps.`**
    
- **`Learn more about enabling ESM Apps service at https://ubuntu.com/esm`**: Tương tự như trên, thông báo về các bản vá bảo mật bổ sung thông qua dịch vụ trả phí ESM.
    
- **`Last login: Mon Jun 30 15:24:55 2025 from 192.168.54.143`**: Dòng này cho biết lần cuối cùng có người đăng nhập vào server này là vào Thứ Hai, ngày 30 tháng 6 năm 2025, lúc 15:24:55 (theo giờ server) từ địa chỉ IP `192.168.54.143`. Đây có thể là địa chỉ IP nội bộ của máy tính của "H" hoặc một thiết bị khác trong mạng cục bộ.
    
- **`rnd@rnd-Default-string:~$`**: **Đây chính là dấu nhắc lệnh của bạn!**
    
    - `rnd`: Tên người dùng mà bạn đã đăng nhập.
        
    - `rnd-Default-string`: Tên máy chủ (hostname) của server.
        
    - `~`: Biểu thị bạn đang ở trong thư mục gốc của người dùng (`/home/rnd/`).
        
    - `$`: Biểu thị bạn đang đăng nhập với quyền người dùng thông thường (nếu là `#` thì là quyền root).
        

**Bây giờ bạn có thể làm gì?**

Bạn đã có thể điều khiển `rnd-server` thông qua dòng lệnh. Dưới đây là một số lệnh cơ bản bạn có thể thử để bắt đầu:

- **`ls`**: Liệt kê các tệp và thư mục trong thư mục hiện tại.
    
- **`pwd`**: Hiển thị đường dẫn của thư mục hiện tại bạn đang ở.
    
- **`whoami`**: Hiển thị tên người dùng hiện tại của bạn.
    
- **`ip a`**: Hiển thị cấu hình mạng của server.
    
- **`df -h`**: Hiển thị dung lượng ổ đĩa.
    
- **`free -h`**: Hiển thị dung lượng RAM.
    
- **`htop`** (nếu cài đặt) hoặc **`top`**: Xem các tiến trình đang chạy và mức sử dụng tài nguyên.
    
- **`exit`**: Để thoát khỏi phiên SSH và quay lại terminal máy tính của bạn.
    

**Một lần nữa, xin chúc mừng bạn đã khắc phục được vấn đề và kết nối thành công!**

---
![[gõ lệnh ls trong máy servẻ.png]]

Last login: Mon Jun 30 15:24:55 2025 from 192.168.54.143
rnd@rnd-Default-string:~$ ls
 Desktop     Downloads   Music      Public   Templates          'udo systemctl enable anydesk'
 Documents   EVisor      Pictures   snap     thinclient_drives   Videos

