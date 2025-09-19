Chắc chắn rồi! Dựa vào form "Thêm công việc mới" bạn cung cấp, đây là các bộ **test data** (dữ liệu kiểm thử) để kiểm tra các trường hợp khác nhau.

Test data được tạo ra để bao quát các kịch bản chính:

- **Happy Path:** Dữ liệu hợp lệ, kiểm tra xem chức năng có hoạt động đúng như mong đợi không.
    
- **Invalid Data:** Dữ liệu không hợp lệ, kiểm tra xem hệ thống có xử lý lỗi và hiển thị cảnh báo chính xác không.
    
- **Boundary Case:** Dữ liệu biên, kiểm tra các giới hạn của logic (ví dụ: ngày kết thúc trùng ngày bắt đầu).
    

Dưới đây là bảng ví dụ về các bộ test data:

---

### **Bảng Test Data cho Form "Thêm Công Việc Mới"**

| **Mục đích kiểm thử**                                             | **Người thực hiện** | **Mô tả**                          | **Mã dự án** | **Ngày bắt đầu** | **Ngày kết thúc** | **Số giờ** | **Khu vực**     | **Kết quả mong đợi**                                                                     |
| ----------------------------------------------------------------- | ------------------- | ---------------------------------- | ------------ | ---------------- | ----------------- | ---------- | --------------- | ---------------------------------------------------------------------------------------- |
| **1. Dữ liệu hợp lệ (Happy Path)**                                | Nguyễn Văn A        | Hoàn thành báo cáo tuần 4 tháng 9. | DA-2025-Q3   | 22/09/2025       | 26/09/2025        | 40         | Văn phòng chính | Tạo công việc thành công.                                                                |
| **2. Bỏ trống trường bắt buộc (`Mô tả`)**                         | Nguyễn Văn B        | _(Để trống)_                       | DA-2025-Q3   | 22/09/2025       | 26/09/2025        | 40         | Tại nhà         | Hiển thị lỗi: "Vui lòng nhập mô tả".                                                     |
| **3. Bỏ trống trường bắt buộc (`Người thực hiện`)**               | _(Để trống)_        | Sửa lỗi giao diện trang chủ.       | DA-2025-Q4   | 01/10/2025       | 02/10/2025        | 16         | Văn phòng chính | Hiển thị lỗi: "Vui lòng chọn người thực hiện".                                           |
| **4. Logic ngày không hợp lệ (`Ngày kết thúc` < `Ngày bắt đầu`)** | Trần Thị C          | Lên kế hoạch cho sự kiện cuối năm. | DA-2025-Q4   | **05/10/2025**   | **01/10/2025**    | 24         | Văn phòng chính | Hiển thị lỗi: "Ngày kết thúc phải sau hoặc bằng ngày bắt đầu".                           |
| **5. `Số giờ` là số âm**                                          | Lê Văn D            | Đào tạo nhân viên mới.             | DA-HR-01     | 29/09/2025       | 30/09/2025        | **-8**     | Phòng họp       | Hiển thị lỗi: "Số giờ phải là số dương".                                                 |
| **6. `Số giờ` là chữ**                                            | Nguyễn Văn A        | Phân tích yêu cầu khách hàng.      | DA-2025-Q3   | 22/09/2025       | 24/09/2025        | **"abc"**  | Văn phòng chính | Hiển thị lỗi: "Số giờ phải là một con số".                                               |
| **7. Dữ liệu biên (`Ngày kết thúc` = `Ngày bắt đầu`)**            | Trần Thị C          | Họp khẩn với đội dự án.            | DA-2025-Q4   | 25/09/2025       | 25/09/2025        | 2          | Phòng họp       | Tạo công việc thành công.                                                                |
| **8. `Số giờ` bằng 0**                                            | Lê Văn D            | Chuẩn bị tài liệu.                 | DA-HR-01     | 29/09/2025       | 29/09/2025        | **0**      | Tại nhà         | Tùy vào yêu cầu: - Chấp nhận và tạo thành công. - Hoặc báo lỗi: "Số giờ phải lớn hơn 0". |

---

### **Cách sử dụng Test Data này**

1. **Thực thi từng dòng:** Mỗi dòng trong bảng trên tương ứng với một lần bạn điền dữ liệu vào form và nhấn nút "Lưu".
    
2. **So sánh kết quả:** Quan sát kết quả thực tế trên màn hình (thông báo thành công, thông báo lỗi) và so sánh nó với cột "Kết quả mong đợi".
    
3. **Ghi nhận:**
    
    - Nếu kết quả thực tế khớp với kết quả mong đợi, test case đó **Pass (Thành công)**.
        
    - Nếu không khớp, test case đó **Fail (Thất bại)** và bạn đã tìm ra một lỗi (bug) cần báo cáo cho lập trình viên.