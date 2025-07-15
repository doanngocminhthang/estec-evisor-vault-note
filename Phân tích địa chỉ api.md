Chào bạn, đây là một câu hỏi rất phổ biến và là một điểm dễ gây nhầm lẫn khi mới làm việc với Vite.

Câu trả lời ngắn gọn là: **Hai địa chỉ IP đó phục vụ hai mục đích hoàn toàn khác nhau và việc chúng khác nhau là hoàn toàn bình thường.**

Hãy cùng phân tích chi tiết nhé.

---

### **1. http://192.168.190.18:5173 là gì?**

Đây là **địa chỉ của máy chủ phát triển (Dev Server) của Vite**.

- **Nguồn gốc:** Địa chỉ IP 192.168.190.18 là địa chỉ IP mà máy tính của bạn (máy bạn đang chạy lệnh npm run dev) nhận được trong mạng nội bộ (LAN). Máy tính của bạn có thể có nhiều giao diện mạng (Wi-Fi, Ethernet, card mạng ảo của VMWare/VirtualBox...) và Vite đã tự động chọn một trong số đó để hiển thị.
    
- **Mục đích:** Địa chỉ này dùng để các thiết bị khác trong cùng mạng LAN (ví dụ: điện thoại, máy tính bảng, máy tính khác) có thể truy cập vào trang web bạn đang phát triển để kiểm tra giao diện trên nhiều thiết bị.
    
- **Nó KHÔNG liên quan** đến việc frontend của bạn sẽ gọi API ở đâu. Nó chỉ đơn giản là "địa chỉ nhà" của chính ứng dụng frontend đang chạy.
    

### **2. VITE_API_ENDPOINT="http://192.168.54.39:5173" là gì?**

Đây là một **biến môi trường (environment variable)** mà bạn định nghĩa trong file .env.

- **Nguồn gốc:** Bạn tự định nghĩa nó trong file cấu hình (.env).
    
- **Mục đích:** Biến này dùng để **chỉ cho code Javascript bên trong ứng dụng frontend của bạn biết địa chỉ của Backend (API Server) ở đâu**. Khi bạn dùng Axios hoặc fetch để gọi API lấy dữ liệu, nó sẽ gửi request đến địa chỉ http://192.168.54.39:5173 này.
    
- **Nó KHÔNG quyết định** địa chỉ mà Vite sẽ chạy trên đó.
    

### **So sánh bằng một ví dụ dễ hiểu:**

Hãy tưởng tượng:

- **Ứng dụng Frontend của bạn (Vite Dev Server)** là **Ngôi nhà của bạn**. Địa chỉ của nó là 192.168.190.18. Đây là nơi bạn đang ở.
    
- **Ứng dụng Backend (API Server)** là **Bưu điện**. Địa chỉ của nó là 192.168.54.39.
    
- **Biến VITE_API_ENDPOINT** giống như một tờ giấy ghi **địa chỉ của Bưu điện**.
    

Khi bạn (frontend) cần gửi một lá thư (API request) để lấy thông tin, bạn sẽ nhìn vào tờ giấy (VITE_API_ENDPOINT) để biết phải gửi đến địa chỉ nào (192.168.54.39), chứ không phải gửi cho chính mình.

**Địa chỉ nhà của bạn và địa chỉ Bưu điện là hai địa chỉ hoàn toàn khác nhau.**

### **Làm thế nào để thay đổi địa chỉ Network của Vite?**

Nếu bạn thực sự muốn Vite chạy trên một địa chỉ IP cụ thể (ví dụ: bạn muốn nó chạy trên địa chỉ IP của card mạng Wi-Fi thay vì card mạng ảo), bạn có thể cấu hình trong file vite.config.js.

Mở file vite.config.js (hoặc vite.config.ts) và thêm hoặc sửa mục server:

Generated javascript

```
// vite.config.js
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  server: {
    // Thêm các dòng này
    host: true, // hoặc '0.0.0.0'
    // Hoặc nếu bạn muốn ép nó chạy trên một IP cụ thể:
    // host: '192.168.54.39' // LƯU Ý: Chỉ hoạt động nếu máy bạn CÓ địa chỉ IP này.
  }
})
```

Use code [with caution](https://support.google.com/legal/answer/13505487).JavaScript

- host: true hoặc host: '0.0.0.0': Đây là cách phổ biến nhất. Nó sẽ cho phép Vite lắng nghe trên tất cả các giao diện mạng có sẵn. Khi chạy, Vite sẽ liệt kê tất cả các địa chỉ IP mà bạn có thể truy cập.
    
- host: 'địa_chỉ_ip': Ép Vite chỉ chạy trên địa chỉ IP này. **Cảnh báo:** Cách này sẽ thất bại nếu máy tính của bạn không thực sự sở hữu địa chỉ IP đó.
    

### **Tóm tắt:**

1. **Địa chỉ Vite hiển thị (192.168.190.18)**: Là địa chỉ của ứng dụng Frontend đang chạy.
    
2. **Địa chỉ trong file .env (192.168.54.39)**: Là địa chỉ của máy chủ Backend mà Frontend sẽ gọi tới.
    
3. Việc chúng khác nhau là **đúng và bình thường**. Cấu hình của bạn không sai.
    
4. Để thay đổi địa chỉ của Vite, hãy sửa file vite.config.js, không phải file .env.



---


Chắc chắn rồi! Khi bạn gặp vấn đề đăng nhập và nghi ngờ nguyên nhân do địa chỉ IP, có hai khả năng chính gây ra lỗi này. Hãy cùng kiểm tra từng bước một cách có hệ thống.

**Hai khả năng chính:**

1. **Frontend không thể kết nối đến Backend:** Trình duyệt (chạy code Frontend trên máy bạn) không thể "nhìn thấy" hoặc "nói chuyện" được với máy chủ API (Backend).
    
2. **Lỗi CORS (Cross-Origin Resource Sharing):** Backend "nhìn thấy" Frontend, nhưng từ chối yêu cầu vì lý do bảo mật (yêu cầu đến từ một "nguồn gốc" - Origin không được phép).
    

---

### **Hướng dẫn kiểm tra và khắc phục từng bước**

#### **Bước 1: Xác nhận lại địa chỉ IP**

Đầu tiên, hãy chắc chắn rằng các địa chỉ IP bạn đang sử dụng là chính xác.

- **Kiểm tra IP máy bạn (chạy Frontend):**
    
    - Mở **Command Prompt (cmd)** hoặc **PowerShell** trên Windows.
        
    - Gõ lệnh ipconfig và nhấn Enter.
        
    - Tìm dòng IPv4 Address trong phần card mạng bạn đang dùng (thường là "Wireless LAN adapter Wi-Fi" hoặc "Ethernet adapter Ethernet"). Đây chính là địa chỉ IP của máy bạn.
        
    - Ví dụ: IPv4 Address. . . . . . . . . . . : 192.168.1.10
        
- **Kiểm tra IP máy chủ (chạy Backend):**
    
    - Làm tương tự trên máy tính đang chạy Backend.
        
    - **Quan trọng:** Địa chỉ trong file .env của bạn (VITE_API_ENDPOINT="http://192.168.54.39:5173") phải **trùng khớp** với địa chỉ IP của máy chủ Backend.
        

#### **Bước 2: Kiểm tra kết nối mạng (Ping)**

Từ máy tính chạy Frontend (máy của bạn), hãy thử xem có thể "ping" (gửi tín hiệu) đến máy chủ Backend không.

- Mở **Command Prompt (cmd)** trên máy bạn.
    
- Gõ lệnh: ping 192.168.54.39 (thay bằng IP chính xác của máy chủ Backend).
    
- **Kết quả mong muốn:** Bạn sẽ thấy các dòng Reply from 192.168.54.39: ... Điều này có nghĩa là hai máy đã "thông" nhau về mặt mạng.
    
- **Kết quả lỗi:** Nếu bạn thấy Request timed out hoặc Destination host unreachable, nghĩa là có vấn đề về kết nối mạng vật lý.
    
    - **Giải pháp:**
        
        - Đảm bảo cả hai máy tính đang kết nối vào **cùng một mạng Wi-Fi/LAN**.
            
        - Kiểm tra xem có **Tường lửa (Firewall)** nào trên máy chủ Backend đang chặn kết nối đến không. Hãy thử tạm thời tắt Windows Firewall trên máy Backend để kiểm tra.
            
        - Kiểm tra lại dây mạng, bộ phát Wi-Fi.
            

#### **Bước 3: Kiểm tra trong Trình duyệt (Công cụ cho nhà phát triển)**

Đây là bước quan trọng nhất để tìm ra lỗi chính xác.

1. Mở trang đăng nhập của bạn trên trình duyệt (ví dụ: Chrome, Firefox).
    
2. Nhấn phím **F12** để mở **Developer Tools (Công cụ cho nhà phát triển)**.
    
3. Chuyển sang tab **"Network" (Mạng)**.
    
4. Nhập thông tin đăng nhập và nhấn nút "Đăng nhập".
    
5. Bạn sẽ thấy một request mới xuất hiện trong tab Network (thường là login, auth, token...). Hãy click vào nó.
    

**Kịch bản 1: Request có màu đỏ và trạng thái là (failed)**

- **Ý nghĩa:** Trình duyệt không thể gửi request đến Backend.
    
- **Nguyên nhân:** Thường là do các vấn đề ở **Bước 2** (mạng không thông, sai IP, sai port, server backend chưa chạy).
    
- **Kiểm tra:**
    
    - Trong tab Headers của request đó, xem phần Request URL. Nó có chính xác là http://192.168.54.39:5173/api/login (hoặc endpoint tương ứng) không? Nếu sai, hãy kiểm tra lại code gọi API và biến môi trường .env.
        
    - Đảm bảo rằng Backend của bạn đang thực sự chạy trên port 5173.
        

**Kịch bản 2: Request có màu đỏ và lỗi liên quan đến CORS**

Bạn sẽ thấy một lỗi rất đặc trưng trong tab **Console**:  
Access to fetch at 'http://192.168.54.39:5173/api/login' from origin 'http://localhost:5173' has been blocked by CORS policy...

- **Ý nghĩa:** Backend đã nhận được request nhưng đã từ chối vì nó đến từ một "origin" (nguồn gốc) không được phép. Ở đây, origin là địa chỉ của Frontend (http://localhost:5173 hoặc http://192.168.190.18:5173).
    
- **Nguyên nhân:** Backend chưa được cấu hình để cho phép Frontend của bạn gọi API.
    
- **Giải pháp (Cần sửa ở phía Backend):**
    
    - Bạn cần vào code của Backend và cấu hình CORS để chấp nhận các request từ địa chỉ của Frontend.
        
    - **Ví dụ trong Node.js/Express:**
        
        Generated javascript
        
        ```
        const cors = require('cors');
        const app = express();
        
        const allowedOrigins = [
            'http://localhost:5173', // Cho phép khi dev trên máy local
            'http://192.168.190.18:5173' // << THÊM DÒNG NÀY
        ];
        
        app.use(cors({
            origin: function (origin, callback) {
                if (!origin || allowedOrigins.indexOf(origin) !== -1) {
                    callback(null, true);
                } else {
                    callback(new Error('Not allowed by CORS'));
                }
            }
        }));
        ```
        
        Use code [with caution](https://support.google.com/legal/answer/13505487).JavaScript
        
    - **Cách đơn giản nhất để test (không an toàn cho production):** Cho phép tất cả các nguồn.
        
        Generated javascript
        
        ```
        // Trong code Backend
        app.use(cors());
        ```
        
        Use code [with caution](https://support.google.com/legal/answer/13505487).JavaScript
        
    - Sau khi sửa code Backend, bạn **phải khởi động lại server Backend** để thay đổi có hiệu lực.
        

### **Tóm tắt các bước cần làm ngay:**

1. **Kiểm tra IP:** Chạy ipconfig trên cả 2 máy, đảm bảo địa chỉ IP trong file .env của Frontend là chính xác.
    
2. **Kiểm tra kết nối:** Dùng lệnh ping từ máy Frontend đến máy Backend.
    
3. **Kiểm tra lỗi trên trình duyệt (F12 -> Network):**
    
    - Lỗi (failed) -> Vấn đề mạng, sai IP/port.
        
    - Lỗi CORS -> Cần cấu hình lại Backend để cho phép địa chỉ của Frontend.
        

Hãy thực hiện các bước trên, bạn sẽ nhanh chóng tìm ra được nguyên nhân chính xác của vấn đề. Chúc bạn thành công


---
---

  

Chính xác, bạn đã hiểu đúng rồi!

- Terminal bạn đang thấy chính là **Backend** đang chạy.
    
- **Swagger API Doc** (tài liệu API) chính là một dạng **Frontend** đơn giản được backend tự động tạo ra.
    

### **Để mở Swagger API Doc, bạn chỉ cần làm một việc đơn giản:**

1. Mở trình duyệt web của bạn (Chrome, Firefox, Edge...).
    
2. Gõ hoặc dán địa chỉ sau vào thanh địa chỉ của trình duyệt và nhấn Enter:
    
    **http://127.0.0.1:8082/docs**
    

**Điều gì sẽ xảy ra?**

- Trình duyệt của bạn sẽ gửi một yêu cầu GET /docs đến backend.
    
- Bạn sẽ thấy một dòng log mới xuất hiện trong terminal của backend, tương tự như dòng bạn đã thấy: INFO: 127.0.0.1:xxxxx - "GET /docs HTTP/1.1" 200 OK.
    
- Trên màn hình trình duyệt, bạn sẽ thấy một trang web đẹp đẽ với tiêu đề như "FastAPI" hoặc "ESKilnMaster" và danh sách các API (các khối màu xanh, xanh lá, cam...).
    

Đó chính là trang **Swagger API Doc** mà bạn đang tìm kiếm. Từ trang này, bạn có thể:

- Xem tất cả các API mà backend hỗ trợ.
    
- Biết được mỗi API cần dữ liệu đầu vào là gì.
    
- Biết được nó sẽ trả về kết quả như thế nào.
    
- Nhấn nút "Try it out" để chạy thử API ngay trên trình duyệt.

---
---

Chắc chắn rồi! Đây là giải thích chi tiết cho từng phần trên giao diện Swagger UI mà bạn đang thấy.

Bạn đã làm rất tốt! Đây chính là "bảng điều khiển" tương tác của Backend. Trang này được tạo ra tự động từ code FastAPI của bạn, giúp bạn hiểu và thử nghiệm các API một cách cực kỳ trực quan.

Hãy cùng phân tích các thành phần chính trong ảnh:

---

### **1. Phần Tiêu đề**

- **FastAPI**: Tên của framework (bộ công cụ lập trình) được dùng để xây dựng nên backend này.
    
- **0.1.0**: Đây là phiên bản của ứng dụng của bạn, được định nghĩa trong mã nguồn.
    
- **OAS 3.1**: Viết tắt của **O**pen**A**PI **S**pecification phiên bản 3.1. Đây là một tiêu chuẩn quốc tế dùng để mô tả các API. Nhờ tuân theo tiêu chuẩn này, các công cụ như Swagger có thể tự động tạo ra giao diện đẹp đẽ này cho bạn.
    

---

### **2. Phần API Endpoints (Quan trọng nhất)**

Đây là danh sách tất cả các "chức năng" mà backend của bạn cung cấp. Trong trường hợp này, bạn có 2 chức năng chính:

#### **Phân tích một Endpoint:**

Hãy lấy endpoint đầu tiên làm ví dụ: POST /classify_status_predict_trend

- **POST**: Đây là **phương thức HTTP (HTTP Method)**. Nó cho biết hành động của API. POST thường có nghĩa là "Gửi dữ liệu lên cho backend để xử lý hoặc tạo mới một cái gì đó". (Các phương thức phổ biến khác là GET - lấy dữ liệu về, PUT - cập nhật, DELETE - xóa).
    
- **/classify_status_predict_trend**: Đây là **đường dẫn (path)** của API. Đây là địa chỉ cụ thể cho chức năng này.
    
    - **Địa chỉ đầy đủ của API này là:** http://127.0.0.1:8082/classify_status_predict_trend
        
- **Classify Status Predict Trend**: Đây là mô tả ngắn gọn, dễ hiểu về chức năng của API này: "Phân loại trạng thái và dự đoán xu hướng".
    

**Tóm lại, bạn có 2 API:**

1. **POST /classify_status_predict_trend**: Gửi dữ liệu lên để phân loại và dự đoán xu hướng.
    
2. **POST /find_issues**: Gửi dữ liệu lên để tìm kiếm các vấn đề (issues).
    

---

### **3. Phần Schemas (Khuôn mẫu dữ liệu)**

"Schemas" định nghĩa **cấu trúc** hay **khuôn mẫu** của dữ liệu được gửi đi hoặc nhận về từ API. Nó giống như một biểu mẫu (form) quy định bạn phải điền những thông tin gì.

- **StatusRequest**: Đây là **Input Schema (Khuôn mẫu đầu vào)**. Rất có thể đây là cấu trúc dữ liệu mà bạn phải gửi lên cho API /classify_status_predict_trend. Nếu bạn bấm vào để mở rộng (Expand), nó sẽ cho bạn biết bạn cần cung cấp những trường dữ liệu nào (ví dụ: temperature, pressure...).
    
- **HTTPValidationError** và **ValidationError**: Đây là các **Output Schema (Khuôn mẫu đầu ra)**, cụ thể là cho trường hợp có lỗi. Nếu bạn gửi dữ liệu không hợp lệ (ví dụ: thiếu một trường bắt buộc), backend sẽ trả về một thông báo lỗi có cấu trúc được định nghĩa bởi các schema này.
    

---

### **Bước tiếp theo để bạn khám phá:**

Bây giờ, để hiểu rõ hơn, bạn hãy làm như sau:

1. **Bấm vào thanh màu xanh lá** của API /classify_status_predict_trend. Nó sẽ mở rộng ra để hiển thị thông tin chi tiết.
    
2. Bấm vào nút **"Try it out"**.
    
3. Bạn sẽ thấy một ô văn bản (Request body) xuất hiện, bên trong có sẵn một cấu trúc JSON mẫu dựa trên schema StatusRequest.
    
4. Hãy chỉnh sửa các giá trị trong đó (nếu cần) và nhấn nút **"Execute"** màu xanh dương.
    

Hành động này sẽ gửi một yêu cầu thật đến backend. Ngay bên dưới, bạn sẽ thấy kết quả mà backend trả về, bao gồm cả "Response body" (dữ liệu trả về) và "Response code" (mã trạng thái, ví dụ 200 OK là thành công). Đây chính là cốt lõi của việc kiểm thử API

---
---

Chắc chắn rồi! Bức ảnh này cho thấy chi tiết của một API và nó là trọng tâm của việc kiểm thử. Hãy cùng phân tích sâu và vạch ra chiến lược test nhé.

### **I. Phân tích Chi tiết Giao diện**

Đây là giao diện chi tiết của API POST /classify_status_predict_trend.
![[Phân tích địa chỉ api.png]]
#### **1. Parameters (Tham số)**

- **No parameters**: Phần này cho biết API không nhận tham số trên đường dẫn URL (ví dụ: /users/{user_id}). Mọi dữ liệu cần thiết phải được gửi trong phần thân của yêu cầu.
    

#### **2. Request body (Thân yêu cầu)**

- **required**: Chữ màu đỏ này khẳng định rằng bạn **bắt buộc** phải gửi dữ liệu trong thân yêu cầu. Nếu không gửi, API sẽ báo lỗi.
    
- **Example Value / Schema**:
    
    - Đây là phần quan trọng nhất cho việc kiểm thử đầu vào (input). Nó cho bạn thấy một **ví dụ cụ thể** về cấu trúc dữ liệu JSON mà API mong muốn nhận được.
        
    - Cấu trúc này là một đối tượng JSON với rất nhiều cặp "khóa": "giá trị" (key-value pairs), ví dụ: "ActualFuel": 0, "ActualFuelSP": 0,... Tất cả đều là các thông số của lò nung (kiln).
        
    - Đây chính là dữ liệu mà bạn sẽ thay đổi để kiểm thử các trường hợp khác nhau.
        

#### **3. Responses (Các phản hồi có thể xảy ra)**

Phần này mô tả các kết quả mà API có thể trả về, tương ứng với các trường hợp thành công và thất bại.

- **Code 200 - Successful Response**:
    
    - **Ý nghĩa:** API đã nhận và xử lý dữ liệu của bạn thành công.
        
    - **Example Value:** Kết quả trả về sẽ là một chuỗi (string), ví dụ: "Normal", "Warning", "Critical". Đây chính là kết quả dự đoán của mô hình ML.
        
- **Code 422 - Validation Error**:
    
    - **Ý nghĩa:** Dữ liệu bạn gửi lên không hợp lệ. Đây là lỗi từ phía bạn (client-side error).
        
    - **Example Value:** Kết quả trả về sẽ là một đối tượng JSON chi tiết, cho bạn biết chính xác lỗi ở đâu.
        
        - "loc": ["body", "tên_trường_bị_lỗi"]: Cho biết lỗi nằm ở trường nào trong Request body.
            
        - "msg": "Mô tả lỗi": Ví dụ: "value is not a valid integer" (giá trị không phải là số nguyên).
            
        - "type": "Loại lỗi": Ví dụ: "type_error.integer".
            

---

### **II. Chiến lược Kiểm thử để Cover các trường hợp**

Mục tiêu của bạn là đảm bảo API hoạt động đúng trong mọi tình huống có thể xảy ra. Để làm điều này, bạn cần kiểm thử các "ca" (test cases) khác nhau, bao gồm cả các ca thành công (happy path) và các ca thất bại (unhappy path/edge cases).

Dưới đây là một chiến lược kiểm thử toàn diện:

#### **Case 1: Happy Path - Kịch bản thành công**

- **Mục tiêu:** Xác nhận API hoạt động đúng với dữ liệu hợp lệ và trả về kết quả dự đoán chính xác.
    
- **Cách làm:**
    
    1. Nhấn nút **"Try it out"**.
        
    2. Lấy một bộ dữ liệu mẫu mà bạn biết chắc kết quả (ví dụ: bộ dữ liệu mà bạn biết sẽ cho ra "Normal"). Điền các giá trị đó vào Request body.
        
    3. Nhấn **"Execute"**.
        
    4. **Kiểm tra kết quả (Assertions):**
        
        - **Response Code** phải là **200**.
            
        - **Response Body** phải là chuỗi "Normal" (hoặc kết quả đúng bạn mong đợi).
            

#### **Case 2: Unhappy Path - Lỗi xác thực dữ liệu (Validation Errors)**

- **Mục tiêu:** Đảm bảo API xử lý đúng các loại dữ liệu đầu vào không hợp lệ và trả về lỗi 422 với thông báo rõ ràng.
    
- **Cách làm:** Tạo ra nhiều kịch bản con, mỗi kịch bản thử một loại lỗi:
    
    - **Kiểu dữ liệu sai:** Thay vì số 0, hãy thử điền một chuỗi chữ như "abc" vào trường "ActualFuel".
	    - ![[Phân tích địa chỉ api-2.png]]
        
    - **Thiếu trường bắt buộc:** Xóa hoàn toàn một dòng, ví dụ xóa dòng "ActualFuel": 0,.
        - ![[Phân tích địa chỉ api-3.png]]
    - **Thêm trường không mong muốn:** Thêm một dòng mới vào JSON, ví dụ "extra_field": 123.
	    - 
        
    - **Giá trị nằm ngoài biên (Boundary/Edge Cases):** Nếu bạn biết một trường nào đó phải là số dương, hãy thử điền số âm. Ví dụ, thử "ActualFuel": -100.
        
- **Kiểm tra kết quả cho mỗi kịch bản con:**
    
    - **Response Code** phải là **422**.
        
    - **Response Body** phải chứa thông tin lỗi rõ ràng, cho biết lỗi ở trường nào và lý do tại sao.
        

#### **Case 3: Kiểm thử Logic của Mô hình ML (Quan trọng)**

- **Mục tiêu:** Xác nhận rằng mô hình Machine Learning bên trong đang đưa ra dự đoán đúng.
    
- **Cách làm:**
    
    1. Chuẩn bị trước 3 bộ dữ liệu đầu vào (3 Request body khác nhau):
        
        - **Bộ 1:** Dữ liệu tương ứng với trạng thái "Normal".
            
        - **Bộ 2:** Dữ liệu tương ứng với trạng thái "Warning".
            
        - **Bộ 3:** Dữ liệu tương ứng với trạng thái "Critical".
            
    2. Thực thi API 3 lần, mỗi lần với một bộ dữ liệu.
        
- **Kiểm tra kết quả cho mỗi lần:**
    
    - Với Bộ 1, Response Body phải là "Normal".
        
    - Với Bộ 2, Response Body phải là "Warning".
        
    - Với Bộ 3, Response Body phải là "Critical".
        

#### **Case 4: Kiểm thử cấu trúc JSON không hợp lệ**

- **Mục tiêu:** Đảm bảo API xử lý được trường hợp JSON bị lỗi cú pháp.
    
- **Cách làm:**
    
    - Cố tình làm hỏng cấu trúc JSON, ví dụ: xóa một dấu phẩy ,, thiếu một dấu ngoặc nhọn }.
        
- **Kiểm tra kết quả:**
    
    - **Response Code** phải là 422 (hoặc 400 Bad Request tùy theo cách FastAPI xử lý).
        
    - **Response Body** phải báo lỗi về "JSON decode error" hoặc tương tự.
        

**Bằng cách thực hiện các nhóm kiểm thử này, bạn sẽ "cover" được hầu hết các kịch bản quan trọng và có thể tự tin rằng API của mình hoạt động ổn định và chính xác.**


![[Phân tích địa chỉ api-1.png]]