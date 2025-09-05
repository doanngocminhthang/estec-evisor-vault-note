```
Tôi đang làm dự án evisor là một ứng dụng quản lý nội bộ công ty, trong ứng dụng có phần quản lý chấm công, có khả năng ghép các file thành phần : file thành phần là 1 bản kế hoạch thi công trong đó có các cột, các hàng. Nhiệm vụ của chức năng quản lý chấm công là ghép 2 file thành phần tạo ra 1 file tổng hợp tên nhân sự, mã dự án, thời gian làm theo ngày, thời gian làm quá 8 tiếng cho 1 task trong 1 ngày sẽ được bôi đỏ. bằng 8 tiếng màu vàng và dưới 8 tiếng màu xanh.
```

Chào bạn, dựa trên mô tả và các hình ảnh bạn cung cấp, tôi đã hiểu rõ về chức năng "Quản lý chấm công" trong dự án **eVisor** của bạn. Đây là một công cụ rất hữu ích để tự động hóa việc tổng hợp và phân tích kế hoạch làm việc từ nhiều nguồn khác nhau.

Dưới đây là mô tả chi tiết về cách thức hoạt động và logic của chức năng này.

### Mục tiêu chính của chức năng

Mục tiêu là xây dựng một công cụ có khả năng:

1. **Tiếp nhận** nhiều file kế hoạch thi công riêng lẻ (gọi là "file thành phần").
    
2. **Tự động ghép nối** (merge) dữ liệu từ các file này.
    
3. **Tạo ra một file tổng hợp** duy nhất, trình bày chi tiết số giờ làm việc của từng nhân sự, cho từng công việc, theo từng ngày.
    
4. **Áp dụng mã màu** để trực quan hóa khối lượng công việc hàng ngày của nhân sự, giúp người quản lý dễ dàng nhận biết tình trạng quá tải hoặc dưới tải.
    

---

### Luồng hoạt động của người dùng

Dựa vào các hình ảnh, luồng hoạt động sẽ diễn ra như sau:

1. **Truy cập chức năng:** Người dùng đăng nhập vào hệ thống eVisor và điều hướng đến mục **Quản lý kế hoạch làm việc** -> **Quản lý chấm công**.
    
2. **Tải lên File thành phần:** Tại giao diện "Chọn File để tải lên", người dùng sẽ kéo thả hoặc chọn nhiều file kế hoạch thi công (ví dụ: các file Excel có cấu trúc như `image_4c7eb3.png`) vào khu vực "Tải lên các File thành phần".
    
3. **Xử lý và Ghép nối:** Người dùng nhấn nút "Tải lên tất cả file" hoặc một nút tương tự như "Ghép nối & Xử lý". Hệ thống sẽ thực hiện các logic nghiệp vụ ở phía sau (backend).
    
4. **Nhận kết quả:** Hệ thống sẽ tạo ra một file tổng hợp duy nhất (có định dạng như `image_4c7711.png` và `image_4c7ad4.png`). Người dùng có thể xem trước hoặc tải file này về máy.
    

---

### Logic xử lý và Quy tắc nghiệp vụ

Đây là phần cốt lõi của chức năng. Khi người dùng tải file lên, hệ thống sẽ thực hiện các bước sau:

#### 1. Đọc và trích xuất dữ liệu từ File thành phần

Với mỗi file thành phần (như `image_4c7eb3.png`), hệ thống cần đọc từng hàng và lấy ra các thông tin quan trọng:

- **Tên nhân sự thực hiện:** (Cột `ASSIGNEE/NHÂN SỰ THỰC HIỆN`)
    
- **Mã dự án:** (Cột `PROJECT CODE/MÃ DỰ ÁN`)
    
- **Mô tả công việc:** (Cột `DESCRIPTION/MÔ TẢ CÔNG VIỆC`)
    
- **Ngày bắt đầu:** (Cột `PLAN KẾ HOẠCH - Từ`)
    
- **Ngày kết thúc:** (Cột `PLAN KẾ HOẠCH - Đến`)
    
- **Tổng số giờ dự kiến:** (Cột `QTY/SL`)
    

#### 2. Phân bổ giờ làm việc theo ngày

Đây là bước quan trọng nhất. Với mỗi công việc (mỗi hàng trong file thành phần), hệ thống cần phân bổ **Tổng số giờ dự kiến** cho các ngày trong khoảng thời gian từ **Ngày bắt đầu** đến **Ngày kết thúc**.

- **Tính số ngày làm việc:** `Số ngày = (Ngày kết thúc - Ngày bắt đầu) + 1`.
    
- **Tính số giờ trung bình mỗi ngày:** `Số giờ mỗi ngày = Tổng số giờ dự kiến / Số ngày`.
    
    - _Ví dụ:_ Công việc "Lên BOQ tủ rack, tủ trung gian, CT" của anh Lê Vĩnh Hà có tổng cộng **10 giờ**, thực hiện từ `24/03/2025` đến `28/03/2025` (tổng 5 ngày).
        
    - Vậy, số giờ mỗi ngày cho task này là: `10 giờ / 5 ngày = 2 giờ/ngày`.
        

#### 3. Tạo cấu trúc File tổng hợp

Hệ thống sẽ tạo một file mới có cấu trúc như sau:

- **Các cột cố định:** STT, Tên nhân sự, Mã dự án, Mô tả công việc, Tên nhân sự (assignee), Filter, Thời gian bắt đầu, Thời gian kết thúc.
    
- **Các cột động (lịch):** Một chuỗi các cột tương ứng với từng ngày trong khoảng thời gian được phân tích (ví dụ: `2025-05-05`, `2025-05-06`, `2025-05-07`,...).
    

#### 4. Điền dữ liệu và áp dụng mã màu

Hệ thống sẽ duyệt qua từng công việc đã xử lý và điền số giờ làm việc mỗi ngày vào các ô tương ứng trong file tổng hợp.

Đồng thời, hệ thống sẽ áp dụng quy tắc định dạng có điều kiện (conditional formatting) cho các ô chứa số giờ:

- Nếu giá trị trong ô **> 8 giờ** -> **Bôi màu đỏ** (Cảnh báo quá tải).
    
- Nếu giá trị trong ô **= 8 giờ** -> **Bôi màu vàng** (Đạt định mức).
    
- Nếu giá trị trong ô **< 8 giờ** (và > 0) -> **Bôi màu xanh** (Dưới định mức).
    

---

### Gợi ý và hướng phát triển thêm

Để chức năng này hoàn thiện hơn, bạn có thể xem xét các điểm sau:

- **Tổng hợp giờ làm của một nhân sự trong ngày:** Hiện tại, file kết quả đang hiển thị giờ của _từng task_. Nếu một nhân sự làm nhiều task trong cùng một ngày, hệ thống nên có thêm một dòng tổng hợp để tính **tổng số giờ làm của nhân sự đó trong ngày** và áp dụng mã màu trên dòng tổng này. Đây là chỉ số quan trọng nhất để đánh giá workload.
    
- **Loại trừ ngày cuối tuần/ngày lễ:** Khi phân bổ giờ làm, hệ thống nên có tùy chọn bỏ qua các ngày thứ 7, Chủ nhật và các ngày lễ đã được định nghĩa trước để tính toán chính xác hơn.
    
- **Xử lý lỗi và định dạng file:** Cần có cơ chế kiểm tra file đầu vào. Nếu file không đúng định dạng (sai tên cột, sai kiểu dữ liệu ngày tháng), hệ thống phải thông báo lỗi rõ ràng cho người dùng.
    
- **Trực quan hóa dữ liệu (Dashboard):** Từ dữ liệu tổng hợp, có thể xây dựng các biểu đồ để quản lý có cái nhìn tổng quan về hiệu suất dự án, nguồn lực nhân sự, v.v.
    

Chúc dự án eVisor của bạn thành công!

