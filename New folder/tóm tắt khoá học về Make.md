---
dc-link: "[[nghiên cứu make dùng notebook bằng script được lấy từ video youtbe]]"
document-link: "[[notebook-make-analytic]]"
---
Chắc chắn rồi! Dưới đây là bản tóm tắt toàn diện và chi tiết về khóa học Make.com của Ben, được dịch và trình bày bằng tiếng Việt để bạn dễ dàng tham khảo.

### **Tóm tắt Khóa học Toàn diện về Make.com của Ben**

Bản tóm tắt này chắt lọc các khái niệm, module và chiến lược chính từ video, cung cấp một hướng dẫn có cấu trúc về mọi thứ bạn cần biết để xây dựng và bán các giải pháp tự động hóa trên Make.com.

---

### **Phần 1: Nền tảng & Khái niệm chính**

#### **1. Make.com là gì?**

- Là một nền tảng tự động hóa no-code (không cần lập trình) giúp kết nối hàng nghìn phần mềm khác nhau để tự động hóa các tác vụ và quy trình công việc.
    
- AI đã làm cho các nền tảng này mạnh hơn gấp 10-100 lần, cho phép tự động hóa các quy trình phức tạp như nghiên cứu và phân loại khách hàng tiềm năng, chứ không chỉ đơn thuần là truyền dữ liệu.
    

#### **2. So sánh Make.com với các đối thủ (Zapier, n8n)**

- **Zapier:** Dễ sử dụng nhất, nhưng kém linh hoạt và đắt hơn.
    
- **n8n:** Kỹ thuật và linh hoạt nhất, khó học nhất nhưng chi phí vận hành rẻ nhất.
    
- **Make.com:** Nằm ở giữa. Nó thân thiện với người dùng như Zapier nhưng cung cấp sự linh hoạt và hiệu quả về chi phí gần giống n8n, khiến nó trở thành lựa chọn được đề xuất cho người mới bắt đầu không chuyên về kỹ thuật nhưng muốn xây dựng các tự động hóa phức tạp.
    

#### **3. Thuật ngữ chính**

- **Scenario (Kịch bản):** Một quy trình tự động hóa hoặc một luồng công việc duy nhất.
    
- **Module:** Một bước trong kịch bản (ví dụ: một phần mềm, một công cụ).
    
- **Connection (Kết nối):** Liên kết đã được xác thực với một ứng dụng phần mềm (ví dụ: tài khoản Google của bạn).
    
- **Trigger/Webhook (Trình kích hoạt):** Điểm khởi đầu của một kịch bản. Đây là hai cách duy nhất để kích hoạt một quy trình.
    
- **Operation (Thao tác):** Một hành động duy nhất được thực hiện bởi một module. **Giá của Make.com dựa trên số lượng thao tác.**
    

---

### **Phần 2: Các loại & Cấu trúc Dữ liệu (Phần quan trọng nhất!)**

Hiểu cách dữ liệu được cấu trúc là cực kỳ quan trọng để xây dựng và gỡ lỗi các kịch bản tự động hóa. Hầu hết các lỗi đều liên quan đến việc không khớp dữ liệu.

- **Kiểu dữ liệu cơ bản:**
    
    - **String:** Văn bản thuần túy (ví dụ: "Công ty của Ben").
        
    - **Number:** Giá trị số (ví dụ: 1000).
        
    - **Boolean:** True hoặc False (Đúng hoặc Sai), được biểu diễn dưới dạng hộp kiểm (checkbox) trong Make.
        
    - **Date:** Một định dạng ngày/giờ cụ thể.
        
- **Cấu trúc phức tạp:**
    
    - **Array (Mảng):** Một danh sách các mục đơn lẻ. Hãy coi nó như một cột duy nhất trong bảng tính. Trong dữ liệu thô, nó được biểu thị bằng dấu ngoặc vuông [].
        
    - **Object / JSON (Đối tượng):** Một tập hợp các cặp khóa-giá trị cho một mục duy nhất (ví dụ: Tên: Ben, Công ty: XYZ). Hãy coi nó như một hàng với nhiều cột trong bảng tính. Trong dữ liệu thô, nó được biểu thị bằng dấu ngoặc nhọn {}.
        
        - **Trong Make.com, một đối tượng đơn lẻ được gọi là "Bundle".**
            
    - **Collection (Tập hợp):** Một danh sách các mục có cấu trúc. Hãy coi nó như một bảng tính đầy đủ với nhiều hàng và cột.
        
        - **Trong Make.com, đây là kết quả bạn nhận được khi một module trả về nhiều "Bundle".**
            

**Điểm mấu chốt:** Make.com xử lý từng **Bundle** một cách riêng biệt. Nếu một module trả về 11 bundle, module tiếp theo trong chuỗi sẽ chạy 11 lần, mỗi lần cho một bundle.

---

### **Phần 3: Các Module & Kỹ năng Thiết yếu**

Đây là những viên gạch nền tảng cho hầu hết mọi kịch bản tự động hóa.

- **Triggers (Trình kích hoạt):** Cách một kịch bản bắt đầu.
    
    - **Polling Trigger (Biểu tượng đồng hồ):** Kiểm tra dữ liệu mới theo một lịch trình cố định (ví dụ: mỗi 15 phút). Nó tiêu tốn một thao tác mỗi khi chạy, ngay cả khi không có dữ liệu mới.
        
    - **Instant Trigger / Webhook (Biểu tượng tia chớp):** Chạy ngay lập tức khi một sự kiện xảy ra trong ứng dụng khác. Nó hiệu quả hơn vì chỉ chạy khi cần thiết. Nó hoạt động bằng cách cung cấp một URL duy nhất để ứng dụng nguồn gửi dữ liệu đến.
        
- **Filters & Routers (Bộ lọc & Bộ định tuyến):**
    
    - **Filter (Biểu tượng phễu):** Một điều kiện IF đơn giản. Nó chỉ cho phép dữ liệu (một bundle) đi qua bước tiếp theo nếu một điều kiện được đáp ứng (ví dụ: "Lượt xem > 10.000").
        
    - **Router:** Chia kịch bản thành nhiều nhánh. Bạn có thể sử dụng các bộ lọc trên mỗi nhánh để gửi dữ liệu đi theo các hướng khác nhau để xử lý khác nhau.
        
- **HTTP Requests (API tùy chỉnh):**
    
    - Được sử dụng khi một ứng dụng không có trên Make hoặc một hành động cụ thể không được hỗ trợ.
        
    - Yêu cầu bốn thông tin chính (tìm thấy trong tài liệu API):
        
        1. **URL (Endpoint):** Địa chỉ cho hành động cụ thể.
            
        2. **Method (Phương thức):** Hành động bạn muốn làm (GET để lấy dữ liệu, POST để tạo dữ liệu, v.v.).
            
        3. **Headers:** Xác thực (API Key) và Loại nội dung (thường là application/json).
            
        4. **Body (Nội dung):** Dữ liệu thực tế (ở định dạng JSON) bạn đang gửi.
            
- **Scraping (Thu thập dữ liệu):** Trích xuất dữ liệu từ các trang web hoặc mạng xã hội.
    
    - **Trang web đơn giản:** Thường chỉ cần một yêu cầu HTTP GET đơn giản.
        
    - **Mạng xã hội (LinkedIn, v.v.) & Google:** Sử dụng các API chuyên dụng từ các chợ API như **apify** hoặc **RapidAPI**. Đối với Google, **SerpApi** rất tuyệt vời.
        
    - **Trang web phức tạp (có công nghệ chống bot):** Sử dụng các dịch vụ scraping nâng cao như **ScraperFly** hoặc **Firecrawl**.
        
- **Iterators & Aggregators (Bộ lặp & Bộ tổng hợp):**
    
    - **Iterator:** Lấy một **mảng** từ một bundle duy nhất và chia nó thành nhiều bundle riêng biệt, để mỗi mục có thể được xử lý riêng lẻ.
        
    - **Aggregator:** Làm ngược lại. Nó lấy nhiều bundle riêng biệt và gộp chúng lại thành một bundle duy nhất chứa một mảng hoặc một khối văn bản.
        
- **Error Handlers (Bộ xử lý lỗi):**
    
    - Cực kỳ quan trọng để đảm bảo độ tin cậy, đặc biệt là khi làm việc cho khách hàng.
        
    - **Break:** Bộ xử lý phổ biến nhất. Nếu xảy ra lỗi (ví dụ: API bị lỗi), nó sẽ đợi và thử lại thao tác vài lần.
        
    - **Ignore:** Bỏ qua lỗi và tiếp tục luồng công việc. Sử dụng một cách thận trọng.
        
    - **Để sử dụng bộ xử lý lỗi, bạn phải bật "Allow storing of incomplete executions" (Cho phép lưu trữ các lần thực thi chưa hoàn thành) trong cài đặt kịch bản.** Điều này giúp lưu lại dữ liệu từ các lần chạy bị lỗi để bạn có thể giải quyết vấn đề và xử lý lại.
        

---

### **Phần 4: Tích hợp AI**

Đây là nơi bạn có thể thêm trí thông minh và logic phức tạp vào quy trình của mình.

- **Chọn một LLM (Mô hình ngôn ngữ lớn):**
    
    - **Non-Reasoning (GPT-4o, Claude 3.5 Sonnet):** Nhanh hơn, rẻ hơn. Tốt nhất cho các tác vụ đơn giản, có cấu trúc như trích xuất, phân loại và tạo nội dung với các quy tắc chặt chẽ.
        
    - **Reasoning (GPT-4 Turbo):** Chậm hơn, đắt hơn. Tốt nhất cho các tác vụ phức tạp đòi hỏi lập kế hoạch và suy luận, như tạo mã hoặc đánh giá nâng cao.
        
- **Prompting Frameworks (Khung câu lệnh - để đảm bảo độ tin cậy):**
    
    - Bạn cần các câu lệnh (prompt) chặt chẽ, chi tiết cho tự động hóa, không phải các câu lệnh trò chuyện như trong ChatGPT.
        
    - **Long Structured Prompt (Câu lệnh có cấu trúc dài - cho việc tạo nội dung phức tạp):** Sử dụng cho các mô hình non-reasoning.
        
        1. **Role (Vai trò):** "Bạn là một chuyên gia hàng đầu về..."
            
        2. **Objective (Mục tiêu):** Mục tiêu từng bước một.
            
        3. **Context (Bối cảnh):** Tại sao tác vụ này quan trọng.
            
        4. **Instructions (Hướng dẫn):** Các quy tắc chi tiết, định dạng đầu ra (ví dụ: "Luôn trả về định dạng JSON hợp lệ"), và phải làm gì khi có lỗi.
            
        5. **Examples (Ví dụ):** Cung cấp 1-2 ví dụ tốt về đầu vào/đầu ra để định hướng văn phong và cấu trúc.
            
        6. **Variables (Biến số):** Dữ liệu từ các module trước.
            
        7. **Notes (Ghi chú):** Nhắc lại các quy tắc quan trọng nhất ở cuối.
            
    - **Prompt Chaining (Chuỗi câu lệnh):** Chia các tác vụ phức tạp thành nhiều bước AI nhỏ hơn. Ví dụ: một module AI thu thập dữ liệu, module thứ hai tóm tắt nó, và module thứ ba viết một email cá nhân hóa dựa trên bản tóm tắt đó. **"Giải pháp cho các vấn đề của AI thường là dùng nhiều AI hơn."**
        

---

### **Phần 5: Các Tính năng Nâng cao**

- **Functions (Hàm):** Các công cụ tích hợp sẵn để xử lý dữ liệu mà **không** tốn thao tác (operations). Hữu ích để làm sạch văn bản (trim()), chia văn bản thành mảng (split()), hoặc định dạng ngày tháng (addDays(), now()).
    
- **Text Parser (Match Pattern / Regex):** Một cách mạnh mẽ, không dùng AI để trích xuất dữ liệu cụ thể, có định dạng nhất quán từ một văn bản lớn hơn (ví dụ: lấy ID video từ URL YouTube). Bạn có thể sử dụng AI như ChatGPT để tạo mẫu Regex cho bạn.
    

---

### **Câu hỏi thường gặp (FAQ)**

1. **H: Sự khác biệt thực sự giữa Make và Zapier đối với người mới bắt đầu là gì?**
    
    - **Đ:** Zapier đơn giản hơn cho các tác vụ "nếu cái này, thì cái kia". Make.com có giao diện trực quan tốt hơn cho các quy trình phức tạp, nhiều bước với logic rẽ nhánh (router). Make cũng rẻ hơn đáng kể khi sử dụng ở quy mô lớn nhờ giá dựa trên số thao tác.
        
2. **H: "Bundle" và "Collection" khác nhau như thế nào? Điều này khó hiểu.**
    
    - **Đ:** Hãy nghĩ về một bảng tính. Một **bundle** là một hàng duy nhất với tất cả dữ liệu của nó (Tên, Email, Công ty). Một **collection** là toàn bộ bảng gồm nhiều hàng. Make xử lý bảng tính từng hàng (bundle) một.
        
3. **H: Khi nào tôi nên sử dụng trình kích hoạt theo lịch trình so với webhook?**
    
    - **Đ:** Hãy sử dụng **webhook** (trình kích hoạt tức thì) bất cứ khi nào có thể. Nó hiệu quả hơn và cung cấp tự động hóa theo thời gian thực. Chỉ sử dụng **trình kích hoạt theo lịch trình** khi ứng dụng nguồn không hỗ trợ webhook và bạn cần kiểm tra cập nhật định kỳ (ví dụ: "Kiểm tra Google Sheet này mỗi giờ để tìm hàng mới").
        
4. **H: Tại sao tôi cần một Iterator nếu Make đã xử lý các hàng trong Google Sheet của tôi từng cái một?**
    
    - **Đ:** Các module như "Search Rows" của Google Sheets hay "Search Records" của Airtable có sẵn một iterator. Tuy nhiên, nếu bạn nhận được một mảng các mục từ một nguồn khác (như một lệnh gọi API tùy chỉnh hoặc một hàm văn bản), nó sẽ đến dưới dạng một mảng duy nhất bên trong một bundle. Bạn cần sử dụng **Iterator** để chia mảng đó thành nhiều bundle để Make có thể xử lý từng mục riêng biệt.
        
5. **H: Tại sao tôi cần một câu lệnh (prompt) dài và phức tạp như vậy cho AI? Tôi không thể chỉ bảo nó "viết một email" sao?**
    
    - **Đ:** Bạn có thể, nhưng nó sẽ không đáng tin cậy. Đối với một kịch bản chạy hàng trăm lần, bạn cần loại bỏ sự biến thiên. Một câu lệnh có cấu trúc dài với các quy tắc, ví dụ và định dạng đầu ra rõ ràng hoạt động như một "lan can bảo vệ" buộc AI phải tạo ra kết quả nhất quán, chất lượng cao mỗi lần.
        
6. **H: Tôi có cần học lập trình để sử dụng module HTTP hoặc Regex không?**
    
    - **Đ:** Không. Đối với HTTP, tài liệu API của dịch vụ bạn đang kết nối sẽ cung cấp URL, Phương thức và Headers để bạn sao chép và dán. Đối với Regex, bạn chỉ cần hỏi một AI như ChatGPT: "Viết cho tôi một mẫu regex để trích xuất địa chỉ email từ văn bản này," và nó sẽ cung cấp cho bạn mẫu để dán vào Text Parser.
        
7. **H: Bộ xử lý lỗi (Error Handler) để làm gì? Kịch bản của tôi chạy tốt khi tôi thử nghiệm.**
    
    - **Đ:** Kịch bản sẽ thất bại trong thực tế vì những lý do bạn không thể lường trước được (ví dụ: API của bên thứ ba tạm thời ngừng hoạt động, hoặc dữ liệu không mong muốn được gửi đến). Một **Error Handler** ngăn toàn bộ kịch bản dừng lại và mất dữ liệu. Bộ xử lý "Break" sẽ chỉ đơn giản là thử lại, điều này khắc phục hầu hết các sự cố API tạm thời một cách tự động mà bạn không cần phải làm gì. Nó rất cần thiết cho các kịch bản tự động hóa chuyên nghiệp và đáng tin cậy.