![[sơ đồ hoạt động use case lấy từ tài liệu.png]]
**

|                     |                                                                                                                                       |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| ID                  | UC08                                                                                                                                  |
| Tên use case        | Đăng nhập                                                                                                                             |
| Mô tả               | Là một người dùng hệ thống, tôi muốn đăng nhập để thực hiện các chức năng của hệ thống.                                               |
| Tác nhân            | Nhân viên kho, P. KHTT                                                                                                                |
| Độ ưu tiên          | Phải có                                                                                                                               |
| Điều kiện kích hoạt | Người dùng truy cập vào ứng dụng web hoặc ứng dụng trên máy PDA                                                                       |
| Tiền điều kiện      | Máy PDA hoạt động bình thường.<br><br>Người dùng đã được cấp tài khoản (username + password) có phân quyền để đăng nhập vào hệ thống. |

  
  
  

|   |   |
|---|---|
|Hậu điều kiện|Người dùng truy cập hệ thống thành công.|
|Luồng cơ bản|1. Hệ thống hiển thị biểu mẫu đăng nhập.<br>    <br>2. Người dùng nhập tên người dùng<br>    <br><br>(username) và mật khẩu (password), sau đó nhấn nút Đăng nhập.<br><br>3. Hệ thống kiểm tra thông tin được nhập vào hợp lệ.<br>    <br>4. Hệ thống hiển thị trang chủ của ứng dụng.|
|Luồng thay thế|3a. Hệ thống kiểm tra thông tin người dùng nhập vào không hợp lệ.<br><br>4a. Hệ thống hiển thị thông báo “Thông tin đăng nhập không chính xác. Vui lòng nhập lại”.<br><br>Quay lại bước 1.|
|Yêu cầu phi chức năng|1. Giao diện dễ sử dụng.|



**