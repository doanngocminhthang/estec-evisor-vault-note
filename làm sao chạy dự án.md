Để chạy hai dự án này song song, bạn cần khởi động server phát triển (development server) cho mỗi dự án trong một cửa sổ terminal riêng biệt.

Dựa trên hình ảnh, dự án bên trái là **Frontend (Vue.js)** và bên phải là **Backend (Python - FastAPI)**.

---

### ## Bên trái - Frontend (Vue.js) 🚀

Đây là giao diện người dùng, nó sẽ chạy trong trình duyệt.

1. **Mở Terminal:** Mở một terminal mới trong cửa sổ VS Code này (Dùng phím tắt `Ctrl` + `~`).
    
2. **Cài đặt thư viện (nếu là lần đầu):** Nếu bạn chưa chạy dự án này bao giờ, hãy gõ lệnh sau để cài đặt các gói cần thiết từ file `package.json`:
    
    Bash
    
    ```
    npm install
    ```
    
3. **Chạy dự án:** Sau khi cài đặt xong, gõ lệnh sau để khởi động server phát triển:
    
    Bash
    
    ```
    npm run dev
    ```
    
    _(Một số dự án Vue cũ hơn có thể dùng lệnh `npm run serve`)_
    

Sau khi chạy thành công, terminal sẽ hiển thị một địa chỉ URL, thường là **`http://localhost:5173`** hoặc **`http://localhost:8080`**. Bạn mở địa chỉ này trên trình duyệt để xem trang web.

---

### ## Bên phải - Backend (FastAPI) 🐍

Đây là máy chủ xử lý logic và làm việc với cơ sở dữ liệu.

1. **Mở Terminal:** Tương tự, mở terminal trong cửa sổ VS Code này (`Ctrl` + `~`).
    
2. **Kích hoạt môi trường ảo (Rất quan trọng):** Dự án Python của bạn đang sử dụng một môi trường ảo (`venv`). Bạn phải kích hoạt nó trước.
    
    PowerShell
    
    ```
    .\venv\Scripts\activate
    ```
    
    Sau khi chạy lệnh này, bạn sẽ thấy `(venv)` xuất hiện ở đầu dòng lệnh.
    
3. **Cài đặt thư viện (nếu là lần đầu):** Cài đặt các gói Python cần thiết từ file `requirements.txt`:
    
    Bash
    
    ```
    pip install -r requirements.txt
    ```
    
4. **Chạy dự án:** Dùng `uvicorn` để khởi động server FastAPI. Giả sử file chính của bạn tên là `main.py` và biến FastAPI tên là `app`.
    
    Bash
    
    ```
    uvicorn main:app --reload
    ```
    
    - `main:app`: `main` là tên file (không có `.py`), `app` là tên biến FastAPI trong file đó.
        
    - `--reload`: Tự động khởi động lại server mỗi khi bạn lưu thay đổi trong code.
        

Sau khi chạy thành công, terminal sẽ báo server đang chạy ở một địa chỉ, thường là **`http://127.0.0.1:8000`**.

---

### ## Chúng hoạt động cùng nhau như thế nào? ☕

- **Backend** (`localhost:8000`) sẽ cung cấp các API (các điểm cuối để lấy hoặc gửi dữ liệu).
    
- **Frontend** (`localhost:5173`) chạy trên trình duyệt sẽ gửi các yêu cầu (request) đến các API của backend để lấy dữ liệu hiển thị cho người dùng.
    

Bây giờ bạn có thể code ở cả hai dự án. Mỗi khi bạn lưu file, server tương ứng sẽ tự động cập nhật và bạn chỉ cần làm mới trình duyệt để thấy thay đổi.