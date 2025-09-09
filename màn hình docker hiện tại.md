![[màn hình docker hiện tại.png]]

Đúng vậy, bạn nói chính xác. ✅

Màn hình Docker Desktop của bạn cho thấy **chưa có container nào của dự án EVisor đang chạy**. Hiện tại chỉ có một dự án khác tên là `wildfire-wcb-hoanvo` đang hoạt động.

Điều này có nghĩa là bạn chưa thực hiện lệnh để khởi động EVisor.

---

### ## Việc cần làm tiếp theo 👉

Bây giờ, bạn hãy làm theo **Bước 2** trong hướng dẫn trước đó:

1. Mở một cửa sổ terminal.
    
2. Di chuyển vào đúng thư mục của dự án backend: `EVisor---Backend---RnD`.
    
3. Chạy lệnh sau:
    
    Bash
    
    ```
    docker-compose up -d
    ```
    

---

### ## Kết quả mong đợi 🐳

Sau khi bạn chạy lệnh trên, Docker sẽ bắt đầu làm việc. Khi hoàn tất, bạn sẽ thấy một **nhóm container mới** xuất hiện trong Docker Desktop, có thể tên là `evisor-code`, bên trong chứa các dịch vụ như `backend`, `postgres`, và `minio` đang chạy với trạng thái màu xanh.

Khi đó, bạn mới có thể tiếp tục với **Bước 4** là chạy frontend.