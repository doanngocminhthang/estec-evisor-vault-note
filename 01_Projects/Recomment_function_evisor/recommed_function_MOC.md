---
date: 2025-07-11
---
# Nguồn và tài liệu

- Link : D:\ESTEC\00. PROJECTS\10. ESTEC-ECOSYSTEM\02. ESTEC-ECOSYSTEM-DOCS
- Link Canva tham khảo : https://www.canva.com/design/DAGsETHYaWU/0jB0-dtpHJOX0ug7k6vsBg/edit
- Link Google Docs : 

# Các khái niệm chính

### **ĐỀ XUẤT TÍNH NĂNG - MODULE QUẢN LÝ KẾ HOẠCH & ĐIỀU HÀNH SẢN XUẤT**

#### **I. MỤC TIÊU TỔNG THỂ**

Số hóa 100% quy trình từ lập kế hoạch, phân công, thực thi, giám sát đến báo cáo tại xưởng trên một **nền tảng hợp nhất (unified platform)**. Mục tiêu là loại bỏ hoàn toàn việc sử dụng giấy tờ, file Excel rời rạc, cung cấp dữ liệu minh bạch, chính xác theo thời gian thực (real-time) cho mọi cấp quản lý và nhân viên, từ đó tối ưu hóa nguồn lực, giảm sai sót và tăng năng suất.

#### **II. PHÂN TÍCH & ĐỐI CHIẾU (VẤN ĐỀ -> GIẢI PHÁP)**

|   |   |   |
|---|---|---|
|Bất Cập & Khó Khăn Hiện Tại|Mục Tiêu Mong Muốn Tương Ứng|Tính Năng Hệ Thống Đề Xuất (Giải Pháp)|
|**1. Cập nhật tiến độ bằng tay**, chỉ quản lý cập nhật. Thông tin trên bảng trắng & giấy tờ.|Quản lý, theo dõi và **cập nhật tiến độ công việc/dự án** tự động.|**Module Điều Hành Xưởng (Shop Floor Control):** Giao diện trên tablet/mobile cho công nhân tự cập nhật trạng thái công việc (Bắt đầu, Tạm dừng, Hoàn thành) và đính kèm hình ảnh.|
|**2. Quản lý dự án, nhân sự, dụng cụ bằng file Excel** rời rạc, khó theo dõi và tổng hợp.|**Phân công & theo dõi nhân sự**. **Quản lý dụng cụ, thiết bị**, lịch sử sửa chữa, kiểm định.|**Module Quản lý Nguồn lực:** Phân công nhiệm vụ cho nhân sự cụ thể. Quản lý vòng đời thiết bị với cảnh báo bảo trì, kiểm định tự động.|
|**3. Quy trình QC bị dừng**, phải gửi mail thủ công để xin ý kiến.|Quản lý, theo dõi và cập nhật tiến độ công việc **liền mạch**.|**Luồng Phê Duyệt Chất Lượng (Digital QC Workflow):** Checklist kiểm tra điện tử. Tự động thông báo cho QC. QC ghi nhận lỗi, chụp ảnh và gửi yêu cầu xử lý ngay trên hệ thống.|
|**4. Quản lý xuất hàng trên 1Office chưa tiện**. Khó theo dõi vật tư cho dự án.|**Quản lý vật tư đầu vào – đầu ra** của dự án.|**Tích hợp Kho & Sản xuất:** Tự động tạo yêu cầu xuất kho vật tư khi lệnh sản xuất được ban hành. Truy vết được vật tư đã dùng cho từng công việc/sản phẩm.|
|**5. Khó tạo báo cáo** khi dữ liệu phân mảnh.|**Tạo báo cáo tùy chỉnh** theo nhu cầu.|**Dashboard & Báo Cáo Thông Minh:** Dashboard trực quan hóa tiến độ, hiệu suất. Khả năng tùy chỉnh và xuất báo cáo tự động (PDF, Excel).|

---

#### **III. CHI TIẾT CÁC NHÓM CHỨC NĂNG ĐỀ XUẤT**

Dưới đây là các nhóm chức năng chi tiết cần xây dựng để đạt được các mục tiêu trên.

**1. Nhóm Chức Năng: Quản lý Kế hoạch & Dự án (Project & Work Order Management)**

- **Tạo và Quản lý Lệnh sản xuất/Dự án:**
    
    - Cho phép tạo mới lệnh sản xuất/dự án với đầy đủ thông tin: Tên, mã dự án, khách hàng, ngày bắt đầu/kết thúc.
        
    - Phân rã công việc thành các nhiệm vụ con (tasks) theo từng công đoạn như trong lưu trình hiện tại (Chuẩn bị, Lắp đặt, Đấu nối, Hoàn thiện, FAT...).
        
- **Thư viện Tài liệu Kỹ thuật số:**
    
    - Đính kèm tất cả các tài liệu liên quan vào từng dự án/nhiệm vụ: BOQ, Spec, Layout, Wiring, bản vẽ...
        
    - Phiên bản hóa tài liệu, đảm bảo nhân viên luôn dùng phiên bản mới nhất.
        

**2. Nhóm Chức Năng: Quản lý Nguồn lực (Resource Management)**

- **Quản lý & Phân công Nhân sự:**
    
    - Tạo hồ sơ nhân sự, ghi nhận kỹ năng, chứng chỉ.
        
    - Giao diện trực quan (kéo-thả) để phân công nhiệm vụ cho từng người hoặc nhóm người.
        
    - Theo dõi tải công việc (workload) của từng nhân viên để tránh chồng chéo hoặc quá tải.
        
- **Quản lý Dụng cụ & Thiết bị (Asset Management):**
    
    - Tạo mã QR/Barcode cho từng thiết bị, dụng cụ.
        
    - Ghi nhận lịch sử sử dụng, sửa chữa, bảo trì, kiểm định.
        
    - **Cảnh báo tự động:** Gửi thông báo khi sắp đến hạn kiểm định, bảo dưỡng.
        

**3. Nhóm Chức Năng: Điều hành & Tương tác tại Xưởng (Shop Floor Execution & Interaction)**

- **Giao diện cho Công nhân trên Tablet/Mobile:**
    
    - Thiết kế đơn giản, dễ sử dụng.
        
    - Hiển thị danh sách công việc được giao trong ngày/tuần.
        
    - Cho phép xem tài liệu, bản vẽ trực tiếp trên thiết bị.
        
- **Cập nhật Tiến độ Real-time:**
    
    - Công nhân check-in/check-out khi bắt đầu/kết thúc một công việc.
        
    - Cập nhật trạng thái: Mới, Đang làm, Tạm dừng, Chờ QC, Hoàn thành.
        
    - Chụp và tải lên hình ảnh tiến độ thực tế.
        
- **Yêu cầu Vật tư Điện tử:**
    
    - Tạo yêu cầu xuất vật tư từ tablet, gửi thẳng đến bộ phận kho.
        

**4. Nhóm Chức Năng: Tích hợp Quản lý Chất lượng (Integrated Quality Control)**

- **Checklist Kiểm tra Điện tử:**
    
    - Số hóa các form kiểm tra (WS-HD-01, QC-P03-01...).
        
    - Nhân viên QC thực hiện kiểm tra và tick ngay trên tablet.
        
- **Quản lý Sự không Phù hợp (Non-conformance Management):**
    
    - Khi phát hiện lỗi, QC có thể tạo một "Báo cáo lỗi" ngay lập tức, đính kèm ảnh, mô tả chi tiết.
        
    - Hệ thống tự động thông báo cho quản lý xưởng và người chịu trách nhiệm để xử lý.
        

**5. Nhóm Chức Năng: Dashboard & Báo cáo (Analytics & Reporting)**

- **Dashboard Giám sát Trực quan:**
    
    - Hiển thị tổng quan tiến độ tất cả các dự án.
        
    - Biểu đồ hiệu suất nhân viên, hiệu suất sử dụng máy móc.
        
    - Cảnh báo các công việc/dự án đang bị chậm tiến độ.
        
- **Báo cáo Tùy chỉnh:**
    
    - Tạo báo cáo tổng kết dự án, báo cáo hiệu suất, báo cáo vật tư...
        
    - Khả năng lọc theo thời gian, nhân viên, dự án và xuất ra các định dạng phổ biến.

---

### **ĐỀ XUẤT TÍNH NĂNG - MODULE QUẢN LÝ THIẾT BỊ & VẬT TƯ (ASSET & SPARE PARTS MANAGEMENT)**

#### **I. MỤC TIÊU TỔNG THỂ**

Số hóa toàn bộ vòng đời của thiết bị, dụng cụ và vật tư phụ tùng tại xưởng. Mục tiêu là cung cấp một **hệ thống quản lý tập trung**, giúp theo dõi chính xác vị trí, tình trạng, lịch sử sử dụng và lịch trình bảo trì của mọi tài sản. Điều này nhằm **loại bỏ việc quản lý bằng file Excel**, đảm bảo thiết bị luôn sẵn sàng, giảm thiểu thời gian chết (downtime) và tối ưu hóa chi phí tồn kho vật tư.

#### **II. PHÂN TÍCH & ĐỐI CHIẾU (VẤN ĐỀ -> GIẢI PHÁP)**

|   |   |   |
|---|---|---|
|Bất Cập & Khó Khăn Hiện Tại|Mục Tiêu Mong Muốn Tương Ứng|Tính Năng Hệ Thống Đề Xuất (Giải Pháp)|
|**1. Quản lý dụng cụ, thiết bị bằng file Excel**, khó theo dõi ai đang giữ, tình trạng ra sao.|Quản lý dụng cụ, thiết bị tại xưởng và mượn đi công trường, **lịch sử sửa chữa – bảo trì, kiểm định**.|**Module Quản lý Vòng đời Thiết bị (Asset Lifecycle Management):** Số hóa hồ sơ thiết bị, theo dõi trạng thái, vị trí bằng mã QR/Barcode.|
|**2. Không có cảnh báo** đến hạn kiểm định, bảo trì, bảo dưỡng. Dễ bỏ sót, gây rủi ro.|**Cảnh báo trễ tiến độ, chồng chéo nhân sự, hết hạn kiểm định, bảo trì-bảo dưỡng.**|**Module Quản lý Bảo trì (Maintenance Management):** Lập lịch bảo trì định kỳ và cảnh báo tự động qua email/notification khi sắp đến hạn.|
|**3. Không có dữ liệu để phân tích** hiệu suất, chi phí sửa chữa cho từng thiết bị.|**Tạo báo cáo tùy chỉnh** theo nhu cầu.|**Phân tích & Báo cáo Hiệu suất Thiết bị:** Dashboard trực quan hóa chi phí bảo trì, số lần hỏng hóc, thời gian ngừng hoạt động (downtime) của từng thiết bị.|

---

#### **III. CHI TIẾT CÁC NHÓM CHỨC NĂNG ĐỀ XUẤT**

**1. Nhóm Chức Năng: Quản lý Hồ sơ Thiết bị & Dụng cụ (Asset Registry)**

- **Số hóa Hồ sơ Thiết bị:**
    
    - Cho phép tạo một hồ sơ duy nhất cho mỗi thiết bị/dụng cụ với các thông tin chi tiết:
        
        - **Thông tin cơ bản:** Tên, mã tài sản, model, nhà sản xuất, ngày mua, hạn bảo hành.
            
        - **Thông tin kỹ thuật:** Thông số, tài liệu hướng dẫn sử dụng (manual), bản vẽ kỹ thuật đính kèm.
            
        - **Thông tin quản lý:** Vị trí lưu trữ mặc định, người/bộ phận phụ trách.
            
- **Gán Định danh Duy nhất (QR Code / Barcode):**
    
    - Hệ thống có khả năng **tự động tạo (generate) và cho phép in tem QR/Barcode** để dán lên từng thiết bị.
        
    - Việc quét mã sẽ ngay lập tức truy xuất ra hồ sơ đầy đủ của thiết bị trên ứng dụng di động.
        

**2. Nhóm Chức Năng: Quản lý Vận hành & Vị trí (Operations & Tracking)**

- **Theo dõi Trạng thái & Vị trí Real-time:**
    
    - Quản lý các trạng thái của thiết bị: **Sẵn sàng (Available), Đang sử dụng (In-use), Đang bảo trì (Under Maintenance), Hỏng (Broken), Đã thanh lý (Disposed)**.
        
    - **Quy trình Mượn/Trả (Check-out / Check-in):**
        
        - Khi một nhân viên muốn mượn dụng cụ, họ sẽ dùng tablet/điện thoại để **quét mã QR trên thiết bị**.
            
        - Hệ thống ghi nhận: Ai mượn, mượn lúc mấy giờ, cho dự án/công việc nào.
            
        - Khi trả, nhân viên quét lại mã để check-in.
            
    - **Quản lý mượn đi công trường:** Cho phép ghi nhận trạng thái "Đang ở công trường [Tên công trường]" và ngày dự kiến trả.
        

**3. Nhóm Chức Năng: Quản lý Bảo trì, Sửa chữa & Kiểm định (Maintenance Management)**

- **Lập Lịch Bảo trì Định kỳ (Preventive Maintenance):**
    
    - Cho phép thiết lập các kế hoạch bảo trì theo:
        
        - **Thời gian:** Ví dụ: bảo trì hàng tháng, hàng quý.
            
        - **Chỉ số sử dụng:** Ví dụ: bảo trì sau mỗi 500 giờ hoạt động (yêu cầu tích hợp với máy móc).
            
- **Cảnh báo Tự động:**
    
    - Hệ thống **tự động gửi email/thông báo đẩy (notification)** cho người phụ trách trước N ngày khi đến hạn bảo trì hoặc kiểm định.
        
- **Quản lý Sự cố & Sửa chữa (Corrective Maintenance):**
    
    - Khi thiết bị hỏng, bất kỳ nhân viên nào cũng có thể **tạo một "Yêu cầu Sửa chữa"** bằng cách quét mã QR và mô tả sự cố (có thể đính kèm ảnh).
        
    - Yêu cầu này tạo thành một "phiếu công việc" được giao cho đội bảo trì xử lý.
        
- **Lưu trữ Lịch sử:**
    
    - Tất cả các hoạt động bảo trì, sửa chữa, thay thế linh kiện đều được ghi nhận vào lịch sử của thiết bị. Điều này cực kỳ giá trị để phân tích và ra quyết định trong tương lai.
        

**4. Nhóm Chức năng: Quản lý Vật tư Phụ tùng (Spare Parts Management)**

- **Quản lý Tồn kho Vật tư:**
    
    - Tạo danh mục các vật tư, phụ tùng dùng cho việc sửa chữa (VD: vòng bi, dầu nhớt, cầu chì...).
        
    - Theo dõi số lượng tồn kho của từng loại vật tư.
        
- **Tích hợp với Bảo trì:**
    
    - Khi thực hiện một công việc sửa chữa, kỹ thuật viên có thể ghi nhận các vật tư đã sử dụng. Hệ thống sẽ **tự động trừ tồn kho**.
        
- **Cảnh báo Tồn kho Tối thiểu (Min-stock Alert):**
    
    - Thiết lập mức tồn kho tối thiểu cho mỗi loại vật tư. Khi số lượng tồn kho giảm xuống dưới mức này, hệ thống sẽ tự động tạo yêu cầu mua hàng.
        

**5. Nhóm Chức năng: Phân tích & Báo cáo (Analytics & Reporting)**

- **Dashboard Trực quan:**
    
    - Hiển thị tổng quan: số lượng thiết bị theo trạng thái, các thiết bị sắp đến hạn bảo trì, chi phí sửa chữa trong tháng...
        
- **Báo cáo Hiệu suất Thiết bị:**
    
    - **MTBF (Mean Time Between Failures):** Thời gian trung bình giữa các lần hỏng hóc.
        
    - **MTTR (Mean Time To Repair):** Thời gian trung bình để sửa chữa.
        
    - Phân tích chi phí vòng đời của thiết bị (tổng chi phí mua sắm + sửa chữa).
        
- **Báo cáo Tùy chỉnh:** Cho phép lọc và xuất báo cáo về lịch sử bảo trì, tình hình sử dụng dụng cụ...



---


### **ĐỀ XUẤT TÍNH NĂNG - MODULE QUẢN LÝ NHÂN SỰ TẠI XƯỞNG (WORKFORCE MANAGEMENT)**

#### **I. MỤC TIÊU TỔNG THỂ**

Số hóa và tối ưu hóa việc **phân công, theo dõi và đánh giá hiệu suất** của đội ngũ nhân sự tại xưởng. Mục tiêu là đảm bảo "đúng người, đúng việc", minh bạch hóa khối lượng công việc, loại bỏ tình trạng chồng chéo hoặc chờ việc, đồng thời cung cấp dữ liệu khách quan để đánh giá năng lực và hiệu quả làm việc của từng cá nhân.

#### **II. PHÂN TÍCH & ĐỐI CHIẾU (VẤN ĐỀ -> GIẢI PHÁP)**

|   |   |   |
|---|---|---|
|Bất Cập & Khó Khăn Hiện Tại|Mục Tiêu Mong Muốn Tương Ứng|Tính Năng Hệ Thống Đề Xuất (Giải Pháp)|
|**1. Theo dõi nhân sự cho dự án bằng file Excel**. Khó biết ai đang làm gì, ai đang rảnh.|**Phân công & theo dõi nhân sự** đang thực hiện theo dự án/dịch vụ.|**Module Lập lịch & Phân công Công việc (Scheduling & Assignment):** Giao diện trực quan để phân công nhiệm vụ và xem lịch làm việc của toàn đội.|
|**2. Không có dữ liệu để đánh giá khách quan** hiệu suất làm việc của công nhân.|**Quản lý, theo dõi và cập nhật tiến độ công việc** của từng cá nhân.|**Module Theo dõi Thời gian & Hiệu suất (Time Tracking & Performance):** Tự động ghi nhận thời gian làm việc thực tế trên từng nhiệm vụ và so sánh với kế hoạch.|
|**3. Khó khăn trong việc tìm người có kỹ năng phù hợp** cho một công việc cụ thể.|Đảm bảo phân công đúng người, đúng việc, tối ưu hóa nguồn lực.|**Module Quản lý Hồ sơ & Kỹ năng (Profile & Skills Management):** Xây dựng hồ sơ năng lực cho từng nhân viên, giúp hệ thống gợi ý người phù hợp.|
|**4. Thiếu cảnh báo** khi có nguy cơ trễ tiến độ hoặc phân công chồng chéo.|**Cảnh báo trễ tiến độ, chồng chéo nhân sự**.|**Hệ thống Cảnh báo Thông minh:** Tự động gửi thông báo khi một người được phân công quá nhiều việc cùng lúc hoặc khi một nhiệm vụ có nguy cơ trễ hạn.|

---

#### **III. CHI TIẾT CÁC NHÓM CHỨC NĂNG ĐỀ XUẤT**

**1. Nhóm Chức Năng: Quản lý Hồ sơ & Năng lực Nhân sự (Employee Profile & Competency Management)**

- **Tạo Hồ sơ Nhân viên 360 độ:**
    
    - **Thông tin cơ bản:** Tên, mã nhân viên, chức danh, tổ/đội.
        
    - **Hồ sơ Kỹ năng (Skill Matrix):** Cho phép gán các kỹ năng cho từng nhân viên (VD: Hàn 6G, Lắp ráp tủ điện, Lập trình PLC Siemens) và đánh giá cấp độ (VD: Cơ bản, Thành thạo, Chuyên gia).
        
    - **Chứng chỉ & Đào tạo:** Quản lý các chứng chỉ (VD: chứng chỉ an toàn lao động, chứng chỉ nghề) và ngày hết hạn. Hệ thống sẽ tự động cảnh báo khi chứng chỉ sắp hết hạn.
        
- **Quản lý Nhóm/Tổ/Đội:**
    
    - Cho phép tạo các nhóm làm việc linh hoạt (VD: Tổ Lắp ráp, Đội Thi công Dự án A) để dễ dàng phân công công việc cho cả nhóm.
        

**2. Nhóm Chức Năng: Lập lịch & Phân công Công việc (Scheduling & Assignment)**

- **Bảng Phân công Trực quan (Gantt Chart / Calendar View):**
    
    - Hiển thị lịch làm việc của tất cả nhân viên dưới dạng lịch hoặc biểu đồ Gantt.
        
    - Quản lý có thể thấy ngay ai đang rảnh, ai đang bận, và đang làm nhiệm vụ nào.
        
- **Phân công Nhiệm vụ Thông minh:**
    
    - Khi phân công một công việc, quản lý có thể **lọc và tìm kiếm nhân viên theo kỹ năng** cần thiết.
        
    - Hệ thống sẽ **cảnh báo nếu phân công chồng chéo** (giao 2 việc cùng một thời điểm cho 1 người) hoặc **quá tải** (tổng số giờ làm việc được giao trong ngày vượt quá giới hạn).
        
- **Giao việc cho Cá nhân và Nhóm:**
    
    - Cho phép giao một nhiệm vụ cho một người cụ thể hoặc cho cả một nhóm (bất kỳ ai trong nhóm cũng có thể nhận việc).
        

**3. Nhóm Chức Năng: Theo dõi Thời gian & Hiệu suất (Time Tracking & Performance)**

- **Chấm công theo Nhiệm vụ (Task-based Time Tracking):**
    
    - Khi bắt đầu một công việc trên tablet, hệ thống sẽ tự động bắt đầu tính giờ (hoặc công nhân chủ động bấm "Start"). Khi kết thúc, họ bấm "Stop".
        
    - Hệ thống sẽ tự động ghi nhận **thời gian thực tế (actual time)** bỏ ra cho mỗi nhiệm vụ.
        
- **So sánh Kế hoạch vs. Thực tế:**
    
    - Hệ thống sẽ so sánh thời gian thực tế với **thời gian dự kiến (planned time)** đã được thiết lập cho nhiệm vụ đó.
        
- **Dashboard Hiệu suất Nhân sự:**
    
    - Hiển thị các chỉ số đo lường hiệu suất (KPIs) của từng cá nhân/nhóm:
        
        - Tỷ lệ hoàn thành công việc đúng hạn.
            
        - Tổng số giờ làm việc hiệu quả.
            
        - Chênh lệch giữa thời gian kế hoạch và thời gian thực tế.
            

**4. Nhóm Chức năng: Báo cáo & Phân tích (Reporting & Analytics)**

- **Báo cáo Tải công việc (Workload Report):**
    
    - Báo cáo chi tiết về khối lượng công việc của từng nhân viên trong một khoảng thời gian, giúp quản lý cân bằng lại việc phân công.
        
- **Báo cáo Lịch sử Công việc:**
    
    - Truy xuất lại tất cả các công việc mà một nhân viên đã thực hiện, thời gian hoàn thành và kết quả.
        
- **Báo cáo Năng lực & Đào tạo:**
    
    - Báo cáo về tình hình kỹ năng của toàn đội, những kỹ năng nào đang thiếu, và danh sách các chứng chỉ cần được đào tạo lại.


---

### **ĐỀ XUẤT TÍNH NĂNG - MODULE QUẢN LÝ KHO (WMS)**

#### **I. MỤC TIÊU TỔNG THỂ**

Số hóa 100% các nghiệp vụ quản lý kho, từ nhập, xuất, kiểm kê cho đến báo cáo. Mục tiêu là xây dựng một **hệ thống kho thông minh, chính xác và minh bạch**, giúp loại bỏ hoàn toàn việc sử dụng giấy tờ, email và các thao tác thủ công. Hệ thống phải đảm bảo dữ liệu tồn kho luôn **chính xác theo thời gian thực (real-time)**, cho phép truy xuất vị trí hàng hóa tức thì, và tối ưu hóa các hoạt động trong kho để đáp ứng kịp thời, nhanh chóng cho nhu cầu sản xuất.

#### **II. PHÂN TÍCH & ĐỐI CHIẾU (VẤN ĐỀ -> GIẢI PHÁP)**

|   |   |   |
|---|---|---|
|Bất Cập & Khó Khăn Hiện Tại|Mục Tiêu Mong Muốn Tương Ứng|Tính Năng Hệ Thống Đề Xuất (Giải Pháp)|
|**1. Khi cần gấp thiết bị để lắp tủ phải lên BOQ**, không linh hoạt, không nhanh chóng.|**Toàn bộ thiết bị được lưu trữ trên nền tảng**. **Check được số lượng thiết bị, phụ kiện trong kho**.|**Module Quản lý Tồn kho Real-time:** Dữ liệu tồn kho được cập nhật ngay sau mỗi giao dịch. Cho phép tìm kiếm và xem tồn kho của bất kỳ vật tư nào.|
|**2. Phải gửi mail cho phòng mua hàng để xác nhận được xuất kho.** Quy trình chậm.|Đảm bảo luồng thông tin liền mạch, giảm thời gian chờ đợi.|**Module Quản lý Yêu cầu & Phê duyệt Điện tử:** Tích hợp luồng yêu cầu xuất kho từ sản xuất, tự động tạo phiếu và gửi cho quản lý kho phê duyệt ngay trên hệ thống.|
|**3. Không biết chính xác vật tư nằm ở đâu.** Sơ đồ kho dán trên cửa, khó cập nhật.|**Tra cứu được thiết bị nằm ở kệ nào, vị trí nào**.|**Module Quản lý Vị trí Kho (Location Management):** Số hóa sơ đồ kho, gán mã QR/Barcode cho từng vị trí (kệ, tầng, ô). Ghi nhận vị trí chính xác của từng món hàng.|
|**4. Số lượng nhập vào 1Office nhưng không có sự đối chiếu** chặt chẽ, dễ sai lệch.|**Dashboard thể hiện sự chênh lệch nhập xuất kho**. **Báo cáo việc xuất nhập kho theo thiết lập thời gian**.|**Module Báo cáo & Phân tích Thông minh:** Dashboard trực quan hóa các hoạt động kho. Tự động tạo báo cáo nhập-xuất-tồn, báo cáo đối chiếu.|
|**5. Kiểm tra thời gian nhận hàng hóa phải thông qua phòng mua hàng.**|Cung cấp thông tin minh bạch, dễ dàng truy xuất cho các bộ phận liên quan.|**Tích hợp với Module Mua hàng:** Đồng bộ trạng thái đơn hàng mua (PO), cho phép kho theo dõi được lịch dự kiến hàng về.|

---

#### **III. CHI TIẾT CÁC NHÓM CHỨC NĂNG ĐỀ XUẤT**

**1. Nhóm Chức Năng: Quản lý Danh mục & Vị trí Kho (Master Data & Location Management)**

- **Quản lý Danh mục Vật tư (Item Master):**
    
    - Tạo hồ sơ chi tiết cho từng loại vật tư, thiết bị: Mã vật tư, tên, mô tả, đơn vị tính, nhà cung cấp, hình ảnh.
        
    - Phân loại vật tư theo nhóm (VD: thiết bị điện, vật tư cơ khí, vật tư tiêu hao...).
        
- **Số hóa Sơ đồ Kho (Warehouse Layout Digitization):**
    
    - Cho phép định nghĩa cấu trúc kho trên hệ thống: Kho -> Dãy -> Kệ -> Tầng -> Ô (Bin).
        
    - **Tạo và in mã QR/Barcode cho từng vị trí (Bin Location)**. Việc quét mã này sẽ là nền tảng cho mọi hoạt động sau này.
        

**2. Nhóm Chức Năng: Quản lý Nhập Kho (Inbound Logistics)**

- **Quản lý Yêu cầu Nhập kho:**
    
    - Tự động nhận thông tin từ Đơn mua hàng (PO) của bộ phận Mua hàng để tạo "Yêu cầu Nhập kho dự kiến".
        
- **Thực hiện Nhập kho bằng Di động (Mobile Goods Receipt):**
    
    - Nhân viên kho dùng tablet/máy quét mã vạch để thực hiện:
        
        - **Đối chiếu:** Quét mã trên phiếu giao hàng hoặc tìm theo mã PO.
            
        - **Ghi nhận:** Nhập số lượng thực nhận, kiểm tra tình trạng, chụp ảnh hàng hóa nếu có hư hỏng.
            
    - **In tem Nhãn nội bộ:** Hệ thống tự động in tem mã vạch/QR code nội bộ ngay tại kho để dán lên từng sản phẩm/thùng hàng.
        
- **Sắp xếp Hàng hóa Thông minh (Smart Put-away):**
    
    - Sau khi nhập kho, hệ thống sẽ **tự động gợi ý vị trí cất hàng tối ưu** dựa trên các quy tắc được thiết lập sẵn (VD: nhóm hàng, tần suất sử dụng...).
        
    - Nhân viên di chuyển hàng đến vị trí và **quét mã vị trí & mã hàng hóa** để xác nhận. Tồn kho và vị trí được cập nhật ngay lập tức.
        

**3. Nhóm Chức Năng: Quản lý Xuất Kho (Outbound Logistics)**

- **Quản lý Yêu cầu Xuất kho Điện tử:**
    
    - Nhận yêu cầu xuất kho tự động từ Lệnh sản xuất hoặc yêu cầu thủ công từ các bộ phận khác.
        
    - Quản lý kho xem xét và **phê duyệt yêu cầu ngay trên hệ thống**.
        
- **Lấy hàng theo Chỉ dẫn (Guided Picking):**
    
    - Hệ thống tạo ra một "danh sách lấy hàng" (picking list) trên tablet cho nhân viên kho.
        
    - Danh sách này được **sắp xếp theo lộ trình tối ưu nhất** trong kho để giảm thiểu quãng đường di chuyển.
        
    - Nhân viên **quét mã vị trí và mã hàng hóa** để đảm bảo lấy đúng và đủ.
        
- **Quản lý Xuất & Bàn giao:**
    
    - Sau khi lấy hàng, hệ thống tạo một "phiếu xuất kho" điện tử.
        
    - Ghi nhận việc bàn giao cho bộ phận nhận hàng (có thể yêu cầu ký xác nhận điện tử).
        

**4. Nhóm Chức Năng: Kiểm soát Tồn kho (Inventory Control)**

- **Tra cứu Tồn kho Real-time:**
    
    - Cho phép tìm kiếm và xem số lượng tồn kho của bất kỳ vật tư nào trên cả máy tính và thiết bị di động.
        
    - Hiển thị rõ số lượng và **vị trí chính xác** của vật tư đó trong kho.
        
- **Kiểm kê Kho bằng Di động (Mobile Inventory Counting):**
    
    - Hỗ trợ các phương pháp kiểm kê: kiểm kê toàn phần, kiểm kê theo chu kỳ (cycle counting).
        
    - Nhân viên dùng tablet đi đến từng vị trí, quét mã vị trí và quét mã hàng hóa để đếm, nhập số lượng thực tế.
        
    - Hệ thống tự động đối chiếu và tạo báo cáo chênh lệch để xử lý.
        
- **Quản lý Chuyển kho Nội bộ:**
    
    - Ghi nhận các hoạt động di chuyển hàng hóa giữa các vị trí, các kho khác nhau.
        

**5. Nhóm Chức năng: Báo cáo & Phân tích (Analytics & Reporting)**

- **Dashboard Kho vận Trực quan:**
    
    - Hiển thị các chỉ số chính: Tổng giá trị tồn kho, các mặt hàng sắp hết, hoạt động nhập/xuất trong ngày...
        
    - Biểu đồ thể hiện sự chênh lệch nhập-xuất.
        
- **Hệ thống Báo cáo Chuẩn:**
    
    - **Báo cáo Nhập-Xuất-Tồn (NXT):** Báo cáo kinh điển và quan trọng nhất.
        
    - **Báo cáo Tuổi Tồn kho (Inventory Aging Report):** Giúp xác định các mặt hàng tồn kho lâu ngày, chậm luân chuyển.
        
    - **Báo cáo Lịch sử Giao dịch:** Truy xuất lại toàn bộ lịch sử của một vật tư.