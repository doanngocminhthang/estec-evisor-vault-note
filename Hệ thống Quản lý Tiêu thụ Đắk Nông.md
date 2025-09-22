Dưới đây là bản tóm tắt chi tiết các chủ đề chính và các ý tưởng hoặc sự kiện quan trọng nhất từ các nguồn được cung cấp, bao gồm các trích dẫn thích hợp.

## Tài liệu Tóm tắt Chi tiết: Hệ thống Quản lý Tiêu thụ Đắk Nông

### 1. Giới thiệu Dự án và Mục đích

Dự án có tên **"ĐẦU TƯ TIN HỌC HÓA PHỤC VỤ QUẢN TRỊ, ĐIỀU HÀNH SẢN XUẤT"** nhằm mục đích phát triển một phần mềm quản lý tiêu thụ tại **CÔNG TY NHÔM ĐẮK NÔNG-TKV** do **CÔNG TY TNHH KỸ THUẬT CÔNG NGHỆ ĐIỆN TỰ ĐỘNG BIỂN ĐÔNG (ESTEC)** là nhà thầu.

**Mục đích chính của tài liệu này là:** "mô tả các yêu cầu phát triển các chức năng của phần mềm quản lý tiêu thụ. Tài liệu này sau khi hoàn thiện sẽ được sử dụng như là cơ sở cho việc phát triển nghiệm thu phần mềm. Tài liệu này được viết cho người quản lý dự án, nhà thiết kế, nhà phát triển và người kiểm thử hệ thống."

**Mục tiêu nghiệp vụ** của phần mềm là "đảm bảo tính chính xác, tối ưu hóa hiệu quả và đồng thời giảm thiểu chi phí vận hành trong quá trình lưu trữ, nhập/xuất hàng hóa tại nhà máy".

**Tổng quan về phần mềm:** "Phần mềm quản lý tiêu thụ là phần mềm được ESTEC xây dựng và phát triển với mục tiêu cung cấp khả năng ghi nhận, quản lý quá trình tiêu thụ hàng hoá trong vận hành sản xuất, kiểm soát lưu kho, tối ưu chi phí vận hành và cung cấp cho cấp lãnh đạo cái nhìn trực quan,chi tiết hoạt động thương mại của nhà máy. Phần mềm có tính linh hoạt cao, được sử dụng trên đa dạng thiết bị như: máy tính, máy tính bản, điện thoại,… Tương thích với các nền tảng IOs, Android, Windows."

### 2. Yêu cầu Chức năng Chính

Phần mềm được thiết kế với nhiều module chức năng quan trọng để quản lý toàn bộ quy trình tiêu thụ hàng hóa.

#### 2.1. Quản trị Hệ thống

- **Đăng nhập (UC08):** Cho phép người dùng hệ thống (Nhân viên kho, P. KHTT) đăng nhập để thực hiện các chức năng. Yêu cầu "Máy PDA hoạt động bình thường. Người dùng đã được cấp tài khoản (username + password) có phân quyền để đăng nhập vào hệ thống."
	- [[Máy PDA là gì]]
- **Quét QR (UC07):** Cho phép nhân viên kho/KHTT quét mã QR để đọc thông tin đối tượng. Điều kiện tiên quyết là "Máy PDA hoạt động bình thường. Mã QR được đặt cố định, rõ ràng."
- **Phân quyền người dùng (UC24):** Dành cho Quản trị viên để "trao/thu hồi quyền truy cập và sử dụng trên một tài nguyên hệ thống cho người dùng". Có 3 phân loại tài nguyên: danh mục, chức năng, bảng.
- **Quản lý thông tin (UC10):** Bao gồm các chức năng con:
- **Tìm kiếm đối tượng (UC10.1):** Tìm kiếm thông tin đối tượng để thao tác.
- **Thêm đối tượng (UC10.3):** Thêm đối tượng mới vào hệ thống.
- **Xóa đối tượng (UC10.2):** Xóa đối tượng khỏi hệ thống.
- **Sửa đối tượng (UC10.4):** Cập nhật thông tin đối tượng.
- **Quản lý thông tin danh mục:** Kế thừa UC Quản lý thông tin, bao gồm quản lý loại bao, loại sản phẩm, sản phẩm, đơn vị, thiết bị, tổ chức, kho, trạng thái.
- **Quản lý thông tin sản phẩm kế toán:** Kế thừa UC Quản lý thông tin.
- **Quản lý thông tin người dùng:** Kế thừa UC Quản lý thông tin.

#### 2.2. Quản lý Nhập Kho

- **Nhập kho (UC19):** Cho phép nhân viên kho "nhập kho tại chỗ để đưa hàng hóa vào kho hiện tại". Có quy tắc nghiệp vụ quan trọng: "Một bao xả đáy chỉ cho phép đóng bao tối đa 5 lần (số lần đóng lại tối đa là 4). Thông tin tem mới phải trùng khớp với tem cũ về “Sản phẩm”, “Loại sản phẩm”, “Loại bao”."
- **Hạ tải (UC06):** "Khi xuất tiêu thụ cần giảm số lượng hàng hóa cho đơn hàng để đạt khối lượng yêu cầu sau khi cân xe lần 2".
- **In và tạo tem mới (UC15):** Cho phép nhân viên kho "in và tạo các tem mới để thêm tem mới vào hệ thống". Có hai loại tem: "tem cho bao 1 tấn và tem cho bao 50 kg". "Mỗi tem trong hệ thống chỉ đại diện cho một bao 1 tấn duy nhất. Đối với bao 50kg, nhiều bao có thể dùng chung một tem, và việc phân biệt giữa các bao 50kg được thực hiện thủ công bởi người dùng."
- **In tem lại (UC16):** Cho phép nhân viên kho in lại các tem đã có sẵn trong hệ thống.

#### 2.3. Quản lý Xuất Kho

- **Xuất tiêu thụ (UC04):** "Khi cần xuất bán các bao hàng theo đơn hàng đã đặt". Yêu cầu "Trạng thái đơn hàng phải khác “Đã thực hiện”."
- **Nâng tải (UC05):** "Là một nhân viên kho, tôi muốn nâng tải để tăng khối lượng hàng hóa trên xe." Điều kiện tiên quyết: "Đơn hàng vẫn còn hàng hóa chưa vận chuyển. Khối lượng xe sau khi cân lần 2 thấp hơn khối lượng dự kiến cho phép."
- **Xuất đóng lại (UC21):** Cho phép nhân viên kho "xuất các bao hàng bị lỗi ra khỏi kho để đóng lại."

#### 2.4. Quản lý Di chuyển Lưu kho

- **Vận chuyển lưu kho – dỡ (UC20):** Cho phép nhân viên kho "dỡ các bao hàng cần được vận chuyển đi kho khác." Điều kiện tiên quyết: "Tất cả bao hàng đều nằm ở trạng thái “Tồn kho”."
- **Vận chuyển lưu kho – bốc (UC20):** Cho phép nhân viên kho "bốc hàng vào kho" sau khi đã được vận chuyển từ kho khác.

#### 2.5. Nhập tay trường số liệu (UC25)

Cho phép người dùng "nhập liệu biểu mẫu lên hệ thống" cho các dữ liệu như sản phẩm, thiết bị, tổ chức, đơn vị, loại bao, kho. Quy tắc nghiệp vụ bao gồm: "Hệ thống chỉ chấp nhận file có đuôi là .xls hoặc .xlsx. File Excel nhập vào phải theo đúng template hệ thống cung cấp (thứ tự cột, tên cột, kiểu dữ liệu)."

#### 2.6. Quản lý Thông tin Đơn hàng

- **Tra cứu đơn hàng (dành cho khách hàng) (UC14):** Khách hàng có thể "tra cứu đơn hàng để xem thông tin chi tiết của đơn hàng" bằng mã đơn hàng (chuỗi hoặc QR).
- **Truy xuất đơn hàng (nhân viên kho) (UC03):** Nhân viên kho/KHTT có thể "xem lại thông tin của đơn hàng khi biết mã đơn hàng". Các thông tin tìm kiếm bao gồm ngày bắt đầu, ngày kết thúc, trạng thái và mã QR.

#### 2.7. Tra cứu Lịch sử Hàng hóa (truy xuất tem) (UC18)

Cho phép nhân viên kho "tra cứu lịch sử hàng hóa để đọc thông tin chi tiết lịch sử nhật ký của hàng hóa" bằng cách tìm kiếm theo các thông tin hoặc quét mã QR.

### 3. Danh sách Báo cáo và Biên bản Tham khảo

Hệ thống sẽ tạo ra nhiều loại báo cáo và biên bản quan trọng, bao gồm:

1. Báo cáo Nhập Xuất Tồn
2. Báo cáo nghiệm thu và bảng kê
3. Biên bản báo cáo hiện trường
4. Báo cáo nhập xuất (tổng hợp, lũy kế)
5. Báo cáo vận chuyển
6. Báo cáo bốc dỡ sản phẩm theo thiết bị
7. Báo cáo chi tiết theo thiết bị vận chuyển (Palang, Cẩu, Xe nâng)
8. Báo cáo tổng hợp lỗi theo nguyên nhân
9. Bảng biểu thống kê xuất nhập và vận chuyển

### 4. Yêu cầu Phi Chức năng

Các yêu cầu phi chức năng tập trung vào khả năng mở rộng và hiệu suất của hệ thống:

- **NFR1:** "Phần mềm có thể mở rộng kết nối đến phần mềm Kế toán (Dành cho phòng Kế toán)".
- **NFR2:** "Phần mềm có thể lấy dữ liệu đăng kí đơn hàng".
- **NFR3:** "Phần mềm có khả năng truy xuất mở rộng (Dành cho phòng Quản lý chất lượng)".

Ngoài ra, nhiều use case nhấn mạnh các yêu cầu phi chức năng như:

- **Giao diện dễ sử dụng/dễ nhìn, thân thiện.**
- **Thời gian xử lý không quá 5 giây** cho hầu hết các tác vụ.
- **Các bước phân tích QR phải thực hiện nhanh.**

### 5. Sơ đồ Thực thể Kết hợp (ERD)

Tài liệu cung cấp ba cấp độ sơ đồ ERD:

- **Sơ đồ mức quan niệm (Conceptual diagram):** Hiển thị tổng quan các thực thể và mối quan hệ.
- **Sơ đồ mức logic (Logical diagram):** Cung cấp chi tiết hơn về các thuộc tính và khóa.
- **Sơ đồ mức vật lý (Physical diagram):** Chi tiết cấu trúc dữ liệu cho các module cụ thể như Quản lý đơn hàng, Quản lý dữ liệu và Quản lý vận chuyển lưu kho.

### Kết luận

Tài liệu này cung cấp một đặc tả yêu cầu phần mềm toàn diện cho hệ thống quản lý tiêu thụ tại Công ty Nhôm Đắk Nông-TKV, bao gồm các chức năng cốt lõi như quản lý hệ thống, nhập/xuất kho, di chuyển lưu kho, quản lý đơn hàng, và các yêu cầu phi chức năng liên quan đến hiệu suất và khả năng mở rộng. Mục tiêu tổng thể là tối ưu hóa hoạt động và cung cấp cái nhìn chi tiết về thương mại cho lãnh đạo nhà máy.

|   |   |
|---|---|
|Tác nhân|Vai trò và Trách nhiệm chính|
|**Nhân viên kho**|Người dùng chính tại hiện trường, thực hiện các nghiệp vụ cốt lõi như nhập kho, xuất kho, nâng/hạ tải, di chuyển lưu kho, in tem thông qua thiết bị PDA.|
|**P. KHTT (Phòng Kế hoạch Tiêu thụ)**|Tham gia vào các quy trình xuất tiêu thụ, hạ tải và truy xuất thông tin đơn hàng.|
|**Quản trị viên (Administrator)**|Quản lý toàn bộ hệ thống, bao gồm quản lý người dùng, phân quyền, quản lý các danh mục và cấu hình hệ thống.|
|**Khách hàng**|Người dùng bên ngoài, có thể tra cứu thông tin trạng thái đơn hàng của mình thông qua giao diện web mà không cần đăng nhập.|