Chắc chắn rồi! Bạn đang xem xét file Authentication.py, đây là **"trái tim" của toàn bộ hệ thống xác thực người dùng** trong dự án Backend.

Với vai trò là một tester, hiểu rõ file này sẽ cho bạn biết chính xác logic đằng sau việc đăng nhập, đăng xuất, đổi mật khẩu... từ đó giúp bạn thiết kế các kịch bản kiểm thử sâu sắc và hiệu quả hơn.

Hãy cùng "giải phẫu" file này.

---

### **A. Tổng quan: Vai trò và Trách nhiệm của file Authentication.py**

File này chứa các hàm logic nghiệp vụ (business logic) liên quan đến người dùng. Nó trả lời các câu hỏi:

- "Làm thế nào để kiểm tra xem username và password có đúng không?" (Authentication_function)
    
- "Làm thế nào để kiểm tra xem một phiên làm việc có còn hợp lệ không?" (check_session)
    
- "Làm thế nào để đăng xuất một người dùng?" (Authentication_Logout_function)
    
- "Làm thế nào để đổi mật khẩu?" (Authentication_ChangePassword_function)
    

Nó là lớp xử lý logic, được gọi bởi lớp API (main.py).

---

### **B. Phân tích chi tiết từng hàm**

#### **1. Authentication_function(conn, input) (Hàm Đăng nhập)**

Đây là hàm quan trọng nhất và cũng là nơi bạn đã tìm thấy các vấn đề.

- **Đầu vào:**
    
    - conn: Một đối tượng kết nối đến database PostgreSQL đã được mở sẵn.
        
    - input: Một đối tượng Pydantic chứa username và password do người dùng gửi lên.
        
- **Luồng hoạt động (Workflow):**
    
    1. **Truy vấn Database:** Thực hiện một câu lệnh SELECT để tìm một người dùng có cả username VÀ password khớp chính xác.
	    1. [[Giải thích truy vấn database như thế nào]]
        
    2. **Kiểm tra kết quả:**
        
        - **if user: (Tìm thấy người dùng - Đăng nhập thành công):**
            
            - Tạo một session_id ngẫu nhiên duy nhất (dùng uuid.uuid4()).
                
            - Xác định thời gian hết hạn cho phiên đăng nhập (8 tiếng kể từ bây giờ).
                
            - **Hành động quan trọng:** Xóa tất cả các phiên đăng nhập cũ của người dùng này trong bảng Session. Điều này đảm bảo mỗi người dùng chỉ có một phiên đăng nhập tại một thời điểm.
                
            - Lưu phiên đăng nhập mới vào bảng Session với session_id và thời gian hết hạn.
                
            - **Trả về (Return):** Một dictionary chứa status: "success", thông tin người dùng (user_id, avatar, full_name), và quan trọng nhất là session_id.
                
        - **else: (Không tìm thấy người dùng - Đăng nhập thất bại):**
            
            - **Trả về (Return):** Một dictionary chứa status: "error" và thông báo lỗi.
                
- **Điểm cần lưu ý cho Tester:**
    
    - **Lỗ hổng bảo mật:** Mật khẩu được lưu dưới dạng văn bản thuần. Đây là một điểm rủi ro lớn.
        
    - **Quản lý Session:** Logic xóa session cũ trước khi tạo session mới là một điểm cần kiểm thử. Chuyện gì sẽ xảy ra nếu người dùng đăng nhập trên 2 trình duyệt khác nhau? Trình duyệt đầu tiên sẽ bị đăng xuất.
        
    - **Dữ liệu trả về:** Bạn biết chính xác khi đăng nhập thành công, bạn sẽ nhận được các khóa: status, authentication, user_id, avatar, full_name, message, session_id, expires_at. Bài test của bạn cần kiểm tra sự tồn tại của các khóa này.
        

#### **2. check_session(conn, user_id) (Hàm Kiểm tra phiên làm việc)**

Đây là hàm "gác cổng" cho hầu hết các API nghiệp vụ.

- **Đầu vào:**
    
    - conn: Kết nối database.
        
    - user_id: Tên người dùng cần kiểm tra.
        
- **Luồng hoạt động:**
    
    1. **Truy vấn Database:** SELECT "expires_at" từ bảng Session dựa trên user_id.
        
    2. **Kiểm tra kết quả:**
        
        - **if session and session[0] > datetime.now():**: Điều kiện này kiểm tra hai thứ:
            
            1. session: Có tìm thấy phiên làm việc nào không?
                
            2. session[0] > datetime.now(): Thời gian hết hạn (expires_at) có lớn hơn thời gian hiện tại không?
                
        - Nếu cả hai đều đúng, **return True** (phiên hợp lệ).
            
        - Ngược lại, **return False** (phiên không hợp lệ).
            
- **Điểm cần lưu ý cho Tester:**
    
    - Đây là logic cốt lõi của việc bảo vệ API. Bạn cần test cả hai trường hợp:
        
        - Gọi API nghiệp vụ với user_id có session hợp lệ -> Thành công.
            
        - Gọi API nghiệp vụ với user_id không có session hoặc session đã hết hạn -> Thất bại.
            
    - Bạn có thể thao tác trực tiếp với database để "làm giả" một session đã hết hạn và kiểm tra xem hàm này có trả về False không.
        

#### **3. Authentication_Logout_function(conn, input) (Hàm Đăng xuất)**

- **Đầu vào:**
    
    - conn: Kết nối database.
        
    - input: Đối tượng chứa username.
        
- **Luồng hoạt động:**
    
    1. **Truy vấn Database:** Thực hiện một câu lệnh DELETE để xóa tất cả các dòng trong bảng Session có user_id khớp với username được cung cấp.
        
    2. **Trả về (Return):** Một dictionary báo đăng xuất thành công.
        
- **Điểm cần lưu ý cho Tester:**
    
    - Đây là một API "hủy diệt". Sau khi gọi nó, mọi session_id trước đó của người dùng sẽ trở nên vô hiệu.
        
    - **Kịch bản test lý tưởng:** Login -> Lấy session_id -> Gọi check_session -> True -> Logout -> Gọi lại check_session -> **Phải là False**.
        

#### **4. Authentication_ChangePassword_function(conn, input) (Hàm Đổi mật khẩu)**

- **Đầu vào:**
    
    - conn: Kết nối database.
        
    - input: Đối tượng chứa username, password (mật khẩu cũ), newpassword.
        
- **Luồng hoạt động:**
    
    1. **Xác thực người dùng:** Trước tiên, nó chạy một câu SELECT để kiểm tra xem có người dùng nào khớp với username VÀ password (mật khẩu cũ) không.
        
    2. **Kiểm tra kết quả:**
        
        - **if oldpassword: (Xác thực thành công):**
            
            - Thực hiện một câu lệnh UPDATE để cập nhật lại password trong bảng User bằng newpassword.
                
            - **Trả về (Return):** Một dictionary báo đổi mật khẩu thành công.
                
        - **else: (Xác thực thất bại):**
            
            - **Trả về (Return):** Một dictionary báo lỗi "Mật khẩu không đúng!".
                
- **Điểm cần lưu ý cho Tester:**
    
    - Test với mật khẩu cũ đúng và mật khẩu cũ sai.
        
    - Sau khi đổi mật khẩu thành công, hãy thử đăng nhập lại bằng **mật khẩu cũ** -> **Phải thất bại**.
        
    - Sau đó, hãy thử đăng nhập bằng **mật khẩu mới** -> **Phải thành công**.
        

---

### **Tóm tắt: "Bí mật" mà file này tiết lộ cho bạn**

1. **Cơ chế xác thực:** Hệ thống không dùng JWT Token tiêu chuẩn, mà dùng một cơ chế **Session ID** tự quản lý, lưu trong database và có thời hạn 8 tiếng.
    
2. **Tên "Token":** Thứ mà bạn cần tìm sau khi đăng nhập là khóa "session_id", không phải "token".
    
3. **Hàm "Gác cổng":** Hàm check_session là chốt chặn an ninh cho các API quan trọng.
    
4. **Lỗ hổng:** Mật khẩu được lưu dưới dạng plain text.
    
5. **Logic nghiệp vụ:** Bạn biết chính xác các bước mà backend thực hiện (truy vấn, xóa, chèn, cập nhật) cho từng chức năng. Điều này giúp bạn thiết kế các test case "thông minh" hơn, nhắm vào các điểm yếu hoặc các luồng logic phức tạp.