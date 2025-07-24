Tuyệt vời! Postman là một công cụ không thể thiếu của tester. Nó giống như một "con dao Thụy Sĩ" cho việc kiểm thử API.

Hướng dẫn này sẽ giúp bạn đi từ con số không đến việc thực hành kiểm thử API /Login của dự án một cách chuyên nghiệp.

---

### **Bước 0: Chuẩn bị**

1. **Cài đặt Postman:** Nếu chưa có, hãy tải và cài đặt Postman từ trang chủ: [https://www.postman.com/downloads/](https://www.google.com/url?sa=E&q=https%3A%2F%2Fwww.postman.com%2Fdownloads%2F)
    
2. **Khởi động Backend:** Đảm bảo server backend của bạn đang chạy (bằng docker-compose up hoặc uvicorn). API của bạn phải đang "sống" ở địa chỉ http://127.0.0.1:8082.
    

---

### **Bước 1: Tạo một "Yêu cầu" (Request) mới**

Hãy bắt đầu với kịch bản đơn giản nhất: **Đăng nhập thành công**.

1. **Mở Postman.** Giao diện có thể hơi phức tạp lúc đầu, nhưng hãy tập trung vào những phần chính.
    
2. Bấm vào nút **+** để mở một tab mới.
    
3. Bạn sẽ thấy một giao diện để tạo request.
    

---

### **Bước 2: Cấu hình Yêu cầu (Request Configuration)**

Đây là lúc bạn "điền vào phiếu yêu cầu" để gửi đến API.

1. **Chọn Phương thức (Method):** Ở bên trái của thanh URL, chọn POST. Đây là phương thức mà API /Login của bạn sử dụng.
    
2. **Nhập URL:** Gõ địa chỉ đầy đủ của API vào thanh URL:
    
    Generated code
    
    ```
    http://127.0.0.1:8082/Login
    ```
    
    Use code [with caution](https://support.google.com/legal/answer/13505487).
    
3. **Chuẩn bị Dữ liệu gửi đi (Request Body):** API /Login yêu cầu bạn gửi username và password dưới dạng JSON.
    
    - Bên dưới thanh URL, bấm vào tab **Body**.
        
    - Chọn tùy chọn **raw**.
        
    - Ở menu thả xuống bên phải, chọn **JSON**. Điều này bảo Postman rằng bạn đang gửi dữ liệu dạng JSON.
        
    - Trong ô văn bản lớn, nhập nội dung JSON sau (đây là dữ liệu cho kịch bản thành công):
        
        Generated json
        
        ```
        {
            "username": "hoanvlh",
            "password": "Ef27Xw34"
        }
        ```
        
        Use code [with caution](https://support.google.com/legal/answer/13505487).Json
        

Giao diện của bạn bây giờ sẽ trông giống như thế này:

---

### **Bước 3: Gửi Yêu cầu và Phân tích Kết quả**

1. Bấm nút **Send** màu xanh dương lớn. Postman sẽ gửi yêu cầu đến server backend của bạn.
    
2. **Chờ kết quả trả về.** Kết quả sẽ hiển thị ở khu vực phía dưới. Hãy cùng phân tích nó:
    

- **① Vùng Phản hồi (Response):** Toàn bộ khu vực phía dưới là kết quả mà server trả về.
    
- **② Nội dung (Body):** Đây là tab mặc định, hiển thị nội dung JSON mà API trả về.
    
    - **Bạn thấy gì?** { "status": "error", "message": "..." }
        
    - **Phân tích:** À ha! Giống hệt như pytest đã phát hiện, dù gửi thông tin đúng nhưng API vẫn trả về lỗi. Điều này xác nhận lại bug về thiếu dữ liệu user trong DB.
        
- **③ Status Code:**
    
    - **Bạn thấy gì?** Status: 200 OK
        
    - **Phân tích:** Mã trạng thái là 200, thành công.
        
- **④ Thời gian (Time):** Thời gian phản hồi của API (ví dụ: 250 ms).
    
- **⑤ Headers:** Tab này chứa các thông tin metadata của phản hồi, như Content-Type: application/json.
    

---

### **Bước 4: Thực hành các Kịch bản khác**

Bây giờ bạn đã biết cách thực hiện một yêu cầu. Hãy thử các kịch bản khác.

**Kịch bản 2: Đăng nhập sai mật khẩu**

1. Trong tab Body, sửa lại mật khẩu:
    
    Generated json
    
    ```
    {
        "username": "hoanvlh",
        "password": "saimatkhau123"
    }
    ```
    ![[Postman-test.png]]
    Use code [with caution](https://support.google.com/legal/answer/13505487).Json
    
2. Bấm Send.
    
3. **Phân tích kết quả:** Bạn sẽ thấy status code vẫn là 200 OK và body JSON vẫn là báo lỗi. Điều này xác nhận lại phát hiện của pytest về việc API không trả về code 401.
    

**Kịch bản 3: Thiếu trường dữ liệu**

1. Trong tab Body, xóa hoàn toàn dòng password:
    
    Generated json
    
    ```
    {
        "username": "hoanvlh"
    }
    ```
    
    Use code [with caution](https://support.google.com/legal/answer/13505487).Json
    
2. Bấm Send.
    
3. **Phân tích kết quả:**
    
    - Lần này, **Status Code** sẽ là **422 Unprocessable Entity**.
        
    - **Body** sẽ là một JSON chi tiết do FastAPI tự động tạo ra để báo lỗi validation.
        

---

### **Bước 5 (Nâng cao): Lưu Yêu cầu và Tạo Bộ sưu tập (Collection)**

Để không phải gõ lại mỗi lần test, bạn nên lưu các yêu cầu của mình lại.

1. Bên cạnh nút Send, bấm nút **Save**.
    
2. Đặt tên cho yêu cầu, ví dụ: [Success] Login.
    
3. Postman sẽ yêu cầu bạn lưu nó vào một **"Collection"**. Hãy tạo một Collection mới tên là EVisor API Tests.
    
4. Làm tương tự, tạo và lưu các yêu cầu cho các kịch bản khác ([Fail] Wrong Password, [Fail] Missing Field...).
    

**Lợi ích:**

- Bây giờ, ở thanh bên trái của Postman, bạn sẽ thấy Collection EVisor API Tests với danh sách các request đã lưu.
    
- Lần sau, bạn chỉ cần click vào một request và bấm Send mà không cần cấu hình lại.
    
- Bạn có thể chạy toàn bộ Collection chỉ bằng một cú click, giống như chạy pytest!
    

Bằng cách thực hành với Postman như thế này, bạn sẽ có một cảm nhận trực quan và sâu sắc về cách API của mình hoạt động, từ đó bổ sung và hoàn thiện cho các kịch bản kiểm thử tự động bằng pytest.