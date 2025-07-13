---
date: 2025-07-10
---
Chào bạn,

Đây là giải thích chi tiết về sơ đồ "PRODUCTION WORKFLOW" (Quy trình sản xuất) mà bạn đã cung cấp. Sơ đồ này mô tả luồng công việc và sự tương tác giữa các hệ thống khác nhau để hoàn thành một đơn hàng sản xuất.

Quy trình được chia thành 4 cấp độ chính, từ trên xuống dưới:

1. **ESTEC ERP (Enterprise Resource Planning):** Hệ thống hoạch định nguồn lực doanh nghiệp, quản lý tổng thể về kinh doanh, đơn hàng, và tài nguyên.
    
2. **ESTEC Scheduler:** Hệ thống lập kế hoạch sản xuất chi tiết.
    
3. **ESTEC MES (Manufacturing Execution System):** Hệ thống điều hành và thực thi sản xuất, quản lý các hoạt động tại xưởng.
    
4. **ESTEC Workshop:** Xưởng sản xuất, nơi các công việc được thực hiện trên thực tế.
    

Dưới đây là giải thích chi tiết các bước theo luồng đi của mũi tên và các số thứ tự:

**Bắt đầu: Từ Đơn hàng đến Yêu cầu Sản xuất**

- **Sale Order (Đơn đặt hàng):** Quy trình bắt đầu khi có một đơn đặt hàng từ khách hàng (được thể hiện bằng logo Wagner) đi vào hệ thống **ESTEC ERP**.
    
- **Request for Production (Yêu cầu sản xuất):** Dựa trên đơn hàng, hệ thống ERP tạo ra một yêu cầu sản xuất, bao gồm các thông tin chính như: Tên sản phẩm, Số lượng, Mức độ ưu tiên, và Ngày giao hàng.
    

**Giai đoạn Lập kế hoạch và Lên lịch**

- **Bước 1: Create Work Order (Tạo Lệnh sản xuất):** Hệ thống ERP chuyển yêu cầu sản xuất xuống cho **ESTEC MES** để tạo ra một "Lệnh sản xuất" (Work Order). Quá trình này được thực hiện thông qua "BOP Process" (có thể là Bill of Process - Quy trình công nghệ).
    
- **Bước 2: Manage Work Order (Quản lý Lệnh sản xuất):** Tại MES, Lệnh sản xuất được quản lý chi tiết hơn, bao gồm: các bước thực hiện, máy móc, nguyên vật liệu, công cụ, yêu cầu thu thập dữ liệu, hướng dẫn công việc, người thực hiện và kỹ năng yêu cầu.
    
- **Bước 3: Schedule Work Order (Lên lịch cho Lệnh sản xuất):** Thông tin từ Lệnh sản xuất được chuyển đến **ESTEC Scheduler**. Hệ thống này sẽ:
    
    - Kiểm tra Nguyên vật liệu thô trong kho (Check Raw materials in Stock).
        
    - Xem xét các ràng buộc về nhân công (Operator constraints).
        
    - Xem xét các ràng buộc về máy móc (Machine Constraints).
        
    - Kiểm tra tình trạng thiếu hụt/chưa sử dụng (Check Shortage/ Unused). Sau khi xem xét tất cả yếu tố, Scheduler sẽ tạo ra một "Kế hoạch sản xuất" (Schedule).
        
- **Bước 4: Release Schedule (Phát hành Kế hoạch):** Kế hoạch sản xuất sau khi được hoàn thiện sẽ được phát hành.
    

**Giai đoạn Thực thi tại xưởng**

- **Bước 5: Release Work Order (Phát hành Lệnh sản xuất):** Kế hoạch từ Scheduler được gửi ngược lại cho MES. Dựa trên kế hoạch này, MES sẽ chính thức "phát hành" Lệnh sản xuất xuống cho **ESTEC Workshop**.
    
- **Bước 6: Start (Bắt đầu):** Dưới xưởng sản xuất, công việc được bắt đầu, bao gồm các công đoạn:
    
    - **Fabrication:** Chế tạo.
        
    - **Assembly:** Lắp ráp.
        
    - **Testing:** Kiểm tra.
        
- **Bước 7: Work Instruction (Hướng dẫn công việc):** Công nhân tại xưởng sẽ làm theo các hướng dẫn công việc chi tiết đã được định nghĩa trong Lệnh sản xuất.
    
- **Bước 8: Acquire Product Status (Cập nhật Trạng thái Sản phẩm):** Trong quá trình sản xuất, trạng thái của sản phẩm được ghi nhận và cập nhật lại hệ thống (có thể là MES).
    
- **Bước 9: Complete Manufacturing Operation (Hoàn thành Công đoạn Sản xuất):** Công việc sản xuất được hoàn thành tại xưởng.
    

**Tóm tắt:**

Đây là một quy trình sản xuất tự động và số hóa, nơi **ERP** nhận đơn hàng, **MES** chi tiết hóa thành lệnh sản xuất, **Scheduler** tối ưu hóa kế hoạch dựa trên nguồn lực thực tế (vật liệu, máy móc, nhân công), và cuối cùng **MES** điều phối cho **Xưởng** thực hiện. Dữ liệu được luân chuyển liền mạch giữa các hệ thống, giúp quản lý sản xuất hiệu quả, giảm sai sót và tăng năng suất.

Khi bạn thiết kế quy trình mới, bạn có thể xem xét thay thế hoặc cải tiến các bước trong sơ đồ này để phù hợp hơn với nhu cầu của mình. Chúc bạn thành công!


