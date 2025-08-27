![[Phân tích yêu cầu từ Hoài Thanh.png]]

[[ES211-P2505-Yêu cầu Thi công]]


Chào bạn,

Đây là một file ghi chú (notes) dùng để làm rõ các yêu cầu và các bước cần thực hiện cho việc **lập kế hoạch sản xuất một tủ điện**, dựa trên một email yêu cầu thi công đã nhận được.

Dưới đây là phân tích và giải thích chi tiết.

---

### ## A. Bối cảnh chung

- **Tình huống:** Một bộ phận (có thể là Kế hoạch Sản xuất hoặc Kỹ thuật) đã nhận được một email yêu cầu thi công có mã `ES211-P2505`.
    
- **Vấn đề:** Email này **không đầy đủ thông tin**. Cụ thể là nó thiếu thông tin quan trọng nhất: "cần thi công loại tủ điện nào?".
    
- **Mục đích của file ghi chú:** Liệt kê các thông tin và tài liệu cần được cung cấp để có thể tiến hành lập kế hoạch sản xuất cho yêu cầu này.
    

---

### ## B. Phân tích chi tiết từng điểm

#### **Câu hỏi trung tâm (Dòng tiêu đề):**

> "Trong mail ES211-P2505-Yêu cầu Thi công.msg không có thông tin loại tủ điện cần thi công, vậy thông tin này lấy từ đâu?"

- **Giải thích:** Đây là vấn đề cốt lõi. Người nhận yêu cầu không biết phải sản xuất cái gì. Các điểm bên dưới là giải pháp để trả lời câu hỏi này.
    

#### **Điểm 1: Các thông tin cơ bản cần có**

> "Để phục vụ cho việc lập kế hoạch sản xuất cần biết mã dự án, mã tủ điện, khách hàng, ngày giao hàng dự kiến."

- **Giải thích:** Đây là 4 thông tin tối thiểu để xác định một đơn hàng sản xuất. Nó trả lời các câu hỏi:
    
    - Sản xuất cho **dự án nào**? (`mã dự án`)
        
    - Sản xuất **cái gì**? (`mã tủ điện`)
        
    - Sản xuất cho **ai**? (`khách hàng`)
        
    - Sản xuất **khi nào** xong? (`ngày giao hàng`)
        

> [!todo]
> Tài liệu mã tủ điện
> - ES211-P2505-020401 Layout Drawing 6Unit (có đóng dấu Issue for Construction)
> - ES211-P2505-020402 Layout Drawing 18Unit (có đóng dấu Issue for Construction)
> - ES211-P2505-020403 Schematic Diagrams 6Unit (có đóng dấu Issue for Construction)
> - ES211-P2505-020404 Schematic Diagrams 18Unit (có đóng dấu Issue for Construction)

#### **Điểm 2 & 3: Các tài liệu kỹ thuật liên quan**

> "Cung cấp những file đính kèm..." và "Cung cấp thêm các Tài liệu liên quan quy trình thi công..."

- **Giải thích:** Hai điểm này yêu cầu cung cấp các **tài liệu kỹ thuật** để biết cách sản xuất tủ điện.
    
    - **File đính kèm:** Thông tin chi tiết về tủ điện có thể nằm trong các file (bản vẽ, specs...) được đính kèm trong email gốc.
        
    - **Tài liệu quy trình (WS-P01-F02...):** Đây là các mã hiệu của tài liệu hướng dẫn công việc hoặc quy trình vận hành tiêu chuẩn (SOP) của công ty. Điều này có nghĩa là công ty đã có sẵn các quy trình lắp ráp tủ điện theo tiêu chuẩn.
        


> [!note]
> Bổ sung
> - WS-P01-F01
> - WS-P01-F02
> - WS-P01-F03




#### **Điểm 4: Phân tích "Make vs. Buy" (Tự sản xuất hay Mua ngoài)**

> "Công đoạn lắp ráp tủ có bán thành phẩm hoặc cụm lắp ráp nào nhà máy không sản xuất được phải mua từ bên ngoài không. Nếu đặt hàng bên ngoài thì có thông tin Purchased Order (PO) không?"

- **Giải thích:** Đây là một câu hỏi quan trọng trong quản lý sản xuất. Trước khi lắp ráp, cần xác định rõ:
    
    - Những linh kiện/cụm linh kiện nào công ty **tự sản xuất**?
        
    - Những linh kiện/cụm linh kiện nào phải **mua từ nhà cung cấp** bên ngoài?
        
    - Nếu phải mua ngoài, cần có thông tin về **Đơn đặt hàng (Purchase Order - PO)** để theo dõi.

---
---

Dựa trên các nguồn thông tin được cung cấp, quá trình lắp ráp tủ điện tại nhà máy có sử dụng **nhiều bán thành phẩm và cụm lắp ráp được mua từ bên ngoài**. Đồng thời, có **thông tin về Đơn đặt hàng (Purchase Order - PO)** được đề cập rõ ràng.

Dưới đây là chi tiết cụ thể:

• **Các linh kiện/cụm lắp ráp phải mua từ bên ngoài:**

    ◦ Kế hoạch thi công liệt kê rất nhiều hạng mục **thiết bị và vật tư** được lắp đặt, cho thấy chúng là các thành phần được mua sẵn chứ không phải tự sản xuất tại xưởng. Các hạng mục này bao gồm:

        ▪ **Các thiết bị điện tử và điện công nghiệp chính:** ZCT (biến dòng bảo vệ chạm đất), MCT (biến dòng đo lường), MCCB (aptomat khối), MCB (aptomat tép), Biến tần, PLC (Bộ điều khiển logic khả trình), ET, Base, Module IO, Scalance, PS, SO (các module và thành phần liên quan đến PLC). Đây là các thiết bị chuyên dụng, thường được mua từ các nhà sản xuất có thương hiệu.

        ▪ **Các thiết bị phụ trợ và điều khiển:** Đèn tủ, Công tắc hành trình, Máy biến áp (biến áp điều khiển), Cầu chì chống sét, Domino, Quạt, Filter (lọc), TS (công tắc nhiệt độ), Cầu chì đơn, Relay, Đèn báo pha, PAC, ERL.

        ▪ **Vật tư đấu nối và lắp đặt:** Terminal (cầu đấu), Jump (cầu nối), chặn, Cover (nắp), vách ngăn từ các thương hiệu như Phoenix và Hanyoung.

        ▪ Mặc dù máng, rail và busbar có công đoạn **gia công (cắt, uốn)** tại xưởng, nhưng vật liệu thô (như thanh cái busbar) hoặc các bộ phận tiêu chuẩn khác vẫn được xem là hàng hóa mua ngoài.

    ◦ Quy trình thi công tại xưởng cũng đề cập đến việc **kiểm tra hàng hóa đã nhập từ phòng mua hàng/kho** và việc "lắp file tổng hợp các thiết bị vật tư đã về". Điều này xác nhận rằng các thiết bị và vật tư được thu mua thông qua một bộ phận mua hàng.

• **Thông tin về Đơn đặt hàng (Purchase Order - PO):**

    ◦ Trong tài liệu "ES211-P2505-Yêu cầu Thi công.pdf" dành cho dự án "Supply Local Control Station 18 RTGC 2-2 & 6RMQC 2-2", thông tin về Hợp đồng/PO được nêu rõ là **PO No.: 4250000079**. Đây là một mã PO cụ thể cho dự án/dịch vụ, cho thấy việc mua sắm các thiết bị và vật tư cho dự án này được quản lý bằng PO.

    ◦ Hơn nữa, trong tài liệu "Đề xuất tính năng chính MOC.pdf", một tính năng quan trọng được đề xuất cho Module Quản lý Kho là **"Tích hợp với Module Mua hàng: Đồng bộ trạng thái đơn hàng mua (PO), cho phép kho theo dõi được lịch dự kiến hàng về"**. Điều này không chỉ khẳng định sự tồn tại của các PO cho việc mua hàng mà còn cho thấy tầm quan trọng của việc quản lý và theo dõi chúng trong hệ thống sản xuất và kho.

    ◦ Quy trình thi công tại xưởng cũng nhắc đến việc kiểm tra thông tin từ **BOQ (Bill of Quantity)** và **Specification**, là những tài liệu liên quan chặt chẽ đến việc lập kế hoạch mua sắm và đơn đặt hàng.

Tóm lại, nhà máy **chủ yếu lắp ráp các tủ điện từ các linh kiện và cụm lắp ráp mua ngoài** và có một hệ thống quản lý các đơn đặt hàng (PO) để theo dõi quá trình mua sắm này


> [!todo]
> Tài liệu
> PO
> BOQ (Bill of Quantity)
> Specification
> 


---
---

#### **Điểm 5: Kiểm tra Tồn kho Nguyên vật liệu**

> "Trích xuất file excel tồn kho nguyên vật liệu trên 1Office"

- **Giải thích:** Sau khi biết được những gì cần **tự sản xuất** (từ điểm 4), bước tiếp theo là phải kiểm tra xem trong kho có đủ **nguyên vật liệu thô** để sản xuất chúng hay không.
    
- **"1Office"** ở đây có thể là tên một phần mềm quản trị doanh nghiệp (ERP) mà công ty đang sử dụng để quản lý kho.
    
> [!note]
> file excel tồn kho nguyên liệu


---

### ## C. Tóm tắt Luồng công việc

File ghi chú này đang mô tả một luồng công việc chuẩn để chuẩn bị cho sản xuất:

1. **Tiếp nhận Yêu cầu:** Nhận email `ES211-P2505`.
    
2. **Làm rõ Thông tin:** Yêu cầu bổ sung 4 thông tin cơ bản (Dự án, Tủ điện, Khách hàng, Ngày giao).
    
3. **Thu thập Tài liệu Kỹ thuật:** Lấy file đính kèm và các quy trình lắp ráp nội bộ.
    
4. **Phân tích Nguồn cung:** Lên danh sách các bộ phận cần mua ngoài và các bộ phận cần tự sản xuất.
    
5. **Kiểm tra Nguồn lực:**
    
    - Đối với hàng mua ngoài -> Tìm Đơn đặt hàng (PO).
        
    - Đối với hàng tự sản xuất -> Kiểm tra tồn kho nguyên vật liệu.
        
6. **Lập Kế hoạch Sản xuất:** Chỉ sau khi hoàn thành tất cả các bước trên, bộ phận kế hoạch mới có đủ thông tin để lập một kế hoạch sản xuất chi tiết.