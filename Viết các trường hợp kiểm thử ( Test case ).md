Chắc chắn rồi! Dựa trên toàn bộ phân tích về Backend, Frontend và các công cụ bạn có, đây là một danh sách các trường hợp kiểm thử (test cases) toàn diện mà bạn có thể áp dụng ngay cho dự án của mình.

Tôi sẽ chia các test case thành 3 nhóm chính, từ cấp thấp đến cấp cao:

1. **Kiểm thử API (Backend):** Đảm bảo "bộ não" hoạt động chính xác.
    
2. **Kiểm thử Giao diện/Component (Frontend):** Đảm bảo "bộ mặt và tay chân" hiển thị và hoạt động đúng.
    
3. **Kiểm thử Luồng người dùng (End-to-End):** Đảm bảo cả hệ thống phối hợp nhịp nhàng.
    

---

### **I. Kiểm thử API (Dùng Pytest hoặc Postman/Insomnia)**

Đây là nền tảng, đảm bảo logic cốt lõi đúng đắn.

#### **A. Nhóm API Xác thực (Authentication)**

|             |                                      |                                                                                                                 |                                                                                                              |
| ----------- | ------------------------------------ | --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| ID Test     | Mục tiêu kiểm thử                    | Các bước thực hiện                                                                                              | Kết quả mong đợi                                                                                             |
| **AUTH-01** | **Happy Path:** Đăng nhập thành công | Gửi POST /Login với username/password chính xác.                                                                | - Status code: 200 OK.<br>- Response body chứa status: "success" và một token.                               |
| **AUTH-02** | Sai mật khẩu                         | Gửi POST /Login với username đúng, password sai.                                                                | - Status code: 401 Unauthorized (hoặc 200 với status "error").<br>- Message: "Invalid username or password". |
| **AUTH-03** | Thiếu trường dữ liệu                 | Gửi POST /Login chỉ có username.                                                                                | - Status code: 422 Unprocessable Entity.<br>- Response body chỉ rõ lỗi thiếu trường password.                |
| **AUTH-04** | Đăng xuất thành công                 | 1. Login để lấy token.<br>2. Gửi POST /Logout.                                                                  | - Status code: 200 OK.<br>- Response body chứa status: "success".                                            |
| **AUTH-05** | Đổi mật khẩu thành công              | 1. Gửi POST /ChangePassword với username, mật khẩu cũ đúng, mật khẩu mới.<br>2. Thử Login lại với mật khẩu MỚI. | - Lần 1: Status code 200.<br>- Lần 2: Login thành công.                                                      |
| **AUTH-06** | Đổi mật khẩu thất bại (sai pass cũ)  | Gửi POST /ChangePassword với mật khẩu cũ không chính xác.                                                       | - Status code: 401 Unauthorized.<br>- Message: "Mật khẩu cũ không đúng".                                     |

#### **B. Nhóm API Nghiệp vụ (POD TimeTracker)**

|            |                                        |                                                                                             |                                                                                                                    |
| ---------- | -------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| ID Test    | Mục tiêu kiểm thử                      | Các bước thực hiện                                                                          | Kết quả mong đợi                                                                                                   |
| **POD-01** | **Happy Path:** Upload file thành công | Gửi POST /POD_TimeTracker_Upload với 1 hoặc nhiều file Excel hợp lệ.                        | - Status code: 200 OK.<br>- Response body chứa status: "success" và danh sách path_files đã được upload lên MinIO. |
| **POD-02** | Upload file không hợp lệ               | Gửi POST /POD_TimeTracker_Upload với file .txt hoặc .jpg.                                   | API có thể vẫn trả về 200 OK (vì nó chỉ upload), nhưng các bước sau (merge) sẽ báo lỗi.                            |
| **POD-03** | **Happy Path:** Gộp file thành công    | 1. Login.<br>2. Gửi POST /POD_TimeTracker_Merge với user_id và danh sách path_files hợp lệ. | - Status code: 200 OK.<br>- Response body chứa status: "success" và đường dẫn đến file tổng hợp mới.               |
| **POD-04** | Gộp file khi chưa đăng nhập            | Gửi POST /POD_TimeTracker_Merge mà không có session/token hợp lệ.                           | - Status code: 200 OK nhưng body là lỗi, hoặc 401 Unauthorized.<br>- Message: "Phiên làm việc đã hết hạn...".      |
| **POD-05** | Gộp file với đường dẫn không tồn tại   | Gửi POST /POD_TimeTracker_Merge với một đường dẫn file không có trên MinIO.                 | API nên trả về lỗi rõ ràng, ví dụ: "File not found on storage".                                                    |
| **POD-06** | **Happy Path:** Tải file thành công    | 1. Login.<br>2. Gửi POST /POD_TimeTracker_Download với path_file hợp lệ.                    | - Status code: 200 OK.<br>- Response Header chứa Content-Disposition: attachment... để trình duyệt tự tải file về. |

---

### **II. Kiểm thử Giao diện & Component (Dùng trình duyệt và Vue DevTools)**

Tập trung vào sự chính xác của hiển thị và tương tác ở cấp độ nhỏ.

|   |   |   |   |
|---|---|---|---|
|ID Test|Mục tiêu kiểm thử|Các bước thực hiện|Kết quả mong đợi (Quan sát trong Vue DevTools)|
|**UI-01**|**State:** Trạng thái đăng nhập được cập nhật|1. Đăng nhập.<br>2. Mở Vue DevTools, kiểm tra Pinia store auth.|- state của auth store chứa thông tin user và token từ API.<br>- Biến isLoggedIn (nếu có) đổi thành true.|
|**UI-02**|**Reactivity:** Giao diện thay đổi theo state|1. Sau khi đăng nhập.<br>2. Quan sát AppHeader.|- Tên người dùng được hiển thị.<br>- Nút "Login" đổi thành menu người dùng với nút "Logout".|
|**UI-03**|**State:** Thu gọn/Mở rộng Sidebar|1. Click vào nút thu gọn Sidebar.<br>2. Quan sát state của component <App>.|- Biến isSidebarCollapsed đổi giá trị (true/false).<br>- Giao diện sidebar thu vào/mở ra tương ứng.|
|**UI-04**|**State:** Hiển thị trạng thái Loading|1. Click nút "Merge" (một hành động tốn thời gian).<br>2. Quan sát state của component trang.|- Biến isLoading đổi thành true. Giao diện hiển thị spinner/loading.<br>- Sau khi API trả về, isLoading đổi lại thành false. Spinner biến mất.|
|**UI-05**|**Routing:** Điều hướng hoạt động|1. Click vào các mục menu trong <SideBar>.|- URL trên trình duyệt thay đổi.<br>- Component bên trong <RouterView> thay đổi tương ứng.<br>- Biến $route trong Vue DevTools cập nhật đúng path.|
|**UI-06**|**State:** Xử lý lỗi API|1. Dùng Chrome DevTools (tab Network) để chặn một yêu cầu API.<br>2. Thực hiện hành động gọi API đó.|- Một thông báo lỗi (toast, dialog) thân thiện được hiển thị cho người dùng.<br>- Trong state của component/store, một biến lỗi (ví dụ error_message) được cập nhật.|

---

### **III. Kiểm thử Luồng người dùng (End-to-End)**

Mô phỏng lại chính xác cách người dùng sẽ tương tác với hệ thống từ đầu đến cuối.

#### **A. Luồng Xác thực Toàn diện**

1. Mở trang web ở chế độ ẩn danh.
    
2. Cố gắng truy cập trực tiếp vào URL /time-tracking. **=> Kết quả:** Bị tự động chuyển hướng về trang /login.
    
3. Tại trang Login, nhập sai mật khẩu. **=> Kết quả:** Nhận được thông báo lỗi "Sai tên đăng nhập hoặc mật khẩu".
    
4. Nhập đúng thông tin. **=> Kết quả:** Đăng nhập thành công và được chuyển hướng đến trang chính (dashboard hoặc /time-tracking).
    
5. Refresh lại trang (F5). **=> Kết quả:** Vẫn ở trạng thái đăng nhập, không bị đá về trang login.
    
6. Click vào nút Logout. **=> Kết quả:** Được chuyển hướng về trang /login.
    
7. Dùng nút "Back" của trình duyệt. **=> Kết quả:** Không thể quay lại trang trước đó, vẫn ở trang /login.
    

#### **B. Luồng Nghiệp vụ TimeTracker Toàn diện**

1. Thực hiện đăng nhập thành công.
    
2. Điều hướng đến trang "Time Tracker".
    
3. Click nút "Upload", chọn 2 file Excel hợp lệ. **=> Kết quả:** Giao diện hiển thị thông báo upload thành công và liệt kê tên 2 file vừa upload.
    
4. Click nút "Merge". **=> Kết quả:** Giao diện hiển thị trạng thái loading. Sau một lúc, hiển thị thông báo "Gộp file thành công!" và một liên kết để tải file kết quả.
    
5. Click vào liên kết tải về. **=> Kết quả:** Trình duyệt tự động tải xuống một file Excel.
    
6. (Manual) Mở file Excel vừa tải và kiểm tra xem dữ liệu có được gộp đúng như mong đợi không.