Chắc chắn rồi! Dưới đây là giải thích chi tiết, bằng tiếng Việt, cho từng phần của tài liệu hướng dẫn này.

Tài liệu này là một quy trình hoàn chỉnh để triển khai (deploy) và vận hành một dịch vụ Machine Learning (ML) có tên ESKilnMaster---BinhPhuoc---ML lên một máy chủ ảo của Amazon Web Services (AWS), gọi là EC2.

---

### **Tổng quan quy trình**

1. **Kết nối**: Lấy quyền truy cập và kết nối vào máy chủ EC2 từ máy tính cá nhân.
    
2. **Triển khai**: Tải mã nguồn của dự án về máy chủ, cài đặt các thư viện cần thiết.
    
3. **Vận hành**: Chạy dịch vụ ML trên máy chủ.
    
4. **Kiểm tra**: Xác nhận dịch vụ đang hoạt động thông qua API và chạy các bài kiểm thử tự động.
    

---

### **🏭🔥 1. Kết nối đến máy chủ EC2 (Connect to EC2)**

Phần này hướng dẫn cách truy cập vào dòng lệnh (terminal) của máy chủ EC2 từ máy tính của bạn. EC2 là một máy chủ ảo trên đám mây, bạn không thể ngồi trước nó và cắm bàn phím vào được, vì vậy bạn cần kết nối từ xa.

- **Yêu cầu**: Bạn cần có "chìa khóa" để xác thực danh tính. Đây là các file .pem và .ppk.
    
    - .pem (Privacy Enhanced Mail): Là file private key dùng cho các công cụ dòng lệnh trên Linux, macOS, hoặc terminal của VSCode.
        
    - .ppk (PuTTY Private Key): Là định dạng private key riêng của công cụ PuTTY và WinSCP trên Windows.
        
    - **Owner: HoanVoESTEC**: Đây là người chịu trách nhiệm quản lý và cấp các file "chìa khóa" này. Bạn cần liên hệ người này để lấy file.
        
- **Phương pháp 1: Kết nối bằng VSCode (hoặc Terminal)**
    
    - Lệnh: ssh -i "${KEY_SSH}.pem" ubuntu@ec2-${IP_SSH}.${REGION}.compute.amazonaws.com
        
    - **Giải thích:**
        
        - ssh: (Secure Shell) là một giao thức mạng an toàn để truy cập vào máy chủ từ xa.
            
        - -i "${KEY_SSH}.pem": Tùy chọn -i (identity file) chỉ định file "chìa khóa" (.pem) bạn sẽ dùng để xác thực.
            
        - ubuntu: Là tên người dùng (username) mặc định cho các máy chủ EC2 chạy hệ điều hành Ubuntu.
            
        - ec2-${IP_SSH}.${REGION}...: Đây là địa chỉ công khai (public address) của máy chủ EC2.
            
- **Phương pháp 2: Dùng WinSCP để chuyển file (trên Windows)**
    
    - WinSCP là một công cụ có giao diện đồ họa giúp bạn chuyển file giữa máy tính cá nhân và máy chủ một cách an toàn.
        
    - **Cấu hình:**
        
        - File protocol: **SFTP** (SSH File Transfer Protocol) - Giao thức truyền file an toàn.
            
        - Host name: Địa chỉ của máy chủ EC2.
            
        - Port number: **22** - Cổng mặc định cho SSH và SFTP.
            
        - User name: **ubuntu**.
            
        - Private key file: Chọn file .ppk mà bạn đã được cấp.
            
    - **Mục đích**: Bạn sẽ dùng công cụ này để tải thư mục chứa code của dự án từ máy tính của bạn lên máy chủ EC2.
        

---

### **🚀🚧 2. Triển khai ứng dụng trên EC2 (Deployment in EC2)**

Sau khi đã kết nối vào máy chủ EC2 bằng SSH (Phương pháp 1), bạn sẽ thực hiện các lệnh sau ngay trên terminal của EC2.

1. **git clone ...**: Tải mã nguồn của dự án từ kho chứa trên GitHub về máy chủ EC2.
    
2. **cd ESKilnMaster---BinhPhuoc---ML**: Di chuyển vào thư mục dự án vừa tải về.
    
3. **virtualenv env**: Tạo một môi trường ảo (virtual environment) tên là env.
    
    - **Tại sao cần môi trường ảo?** Nó giúp cô lập các thư viện Python của dự án này với các dự án khác trên cùng máy chủ, tránh xung đột phiên bản. Giống như bạn tạo một "căn phòng riêng" cho dự án của mình.
        
4. **source env/bin/activate (Linux) hoặc .\env\Scripts\activate (Windows)**: Kích hoạt môi trường ảo. Sau khi chạy lệnh này, bạn sẽ thấy (env) xuất hiện ở đầu dòng lệnh, cho biết bạn đang ở trong môi trường ảo.
    
    - Lưu ý: Lệnh source .\env\bin\activate trong tài liệu gốc là sự kết hợp sai giữa cú pháp Linux (source) và đường dẫn Windows (.\). Cần dùng đúng lệnh cho hệ điều hành của máy chủ EC2 (thường là Linux).
        
5. **pip install -r requirements.txt**:
    
    - pip: Công cụ quản lý gói của Python.
        
    - requirements.txt: Là một file liệt kê tất cả các thư viện bên ngoài mà dự án cần để chạy.
        
    - Lệnh này sẽ đọc file đó và tự động cài đặt tất cả các thư viện cần thiết vào môi trường ảo đang được kích hoạt.
        

---

### **🐧🪟🏁 3. Khởi động dịch vụ ML trên EC2 (Start ML service in EC2)**

Sau khi cài đặt xong, bây giờ là lúc chạy ứng dụng.

- **Uvicorn**: Là một máy chủ web (web server) hiệu suất cao, được dùng để chạy các ứng dụng Python hiện đại như FastAPI (dự án này có thể được xây dựng bằng FastAPI, dựa trên cú pháp src.main:app).
    
- **🌱 Chế độ Develop (Phát triển):**
    
    - Lệnh: uvicorn src.main:app --port ${PORT} --host ${HOST} --reload
        
    - **Giải thích:**
        
        - src.main:app: Bảo Uvicorn tìm đối tượng tên app trong file src/main.py để chạy.
            
        - --port 8082: Dịch vụ sẽ chạy và lắng nghe ở cổng (port) 8082.
            
        - --host 0.0.0.0: Cho phép các kết nối từ bất kỳ địa chỉ IP nào, giúp bạn có thể truy cập dịch vụ từ bên ngoài máy chủ EC2.
            
        - --reload: Tự động khởi động lại dịch vụ mỗi khi bạn thay đổi mã nguồn. Rất tiện lợi khi đang lập trình, nhưng không nên dùng khi triển khai chính thức.
            
- **🌴 Chế độ Deploy (Triển khai chính thức):**
    
    - Lệnh: nohup uvicorn src.main:app --port ${PORT} --host ${HOST} &
        
    - **Giải thích:**
        
        - nohup (No Hang Up): Đảm bảo tiến trình (process) vẫn tiếp tục chạy ngay cả khi bạn đóng cửa sổ terminal (ngắt kết nối SSH). Đây là lệnh cực kỳ quan trọng khi deploy.
            
        - &: Chạy lệnh trong nền (background), trả lại dấu nhắc lệnh cho bạn ngay lập tức để bạn có thể làm việc khác.
            
- **Quản lý tiến trình:**
    
    - **ps aux | grep 8082**: Tìm kiếm tiến trình đang chạy.
        
        - ps aux: Liệt kê tất cả các tiến trình đang chạy trên hệ thống.
            
        - | grep 8082: Lọc danh sách đó và chỉ hiển thị những dòng có chứa "8082", giúp bạn tìm ra tiến trình của dịch vụ ML. Bạn sẽ thấy một con số gọi là **PID** (Process ID).
            
    - **kill -9 ${PID}**: Dừng dịch vụ.
        
        - kill: Lệnh để gửi tín hiệu đến một tiến trình.
            
        - -9: Là tín hiệu "giết" (FORCE KILL), buộc tiến trình phải dừng ngay lập tức.
            
        - ${PID}: Thay bằng số PID bạn tìm được từ lệnh trên.
            

---

### **🦾 4. Truy cập Swagger APIs từ máy tính cá nhân**

Swagger UI là một giao diện web tự động tạo ra từ mã nguồn của bạn, cho phép bạn xem, tương tác và thử nghiệm các API của dịch vụ một cách trực quan.

- **http://localhost:8082/docs#/**: URL này chỉ hoạt động khi bạn chạy dịch vụ trên **máy tính cá nhân của mình** (localhost).
    
- **http://54.251.242.155:8082/docs#/**: Đây là URL đúng để truy cập dịch vụ đang chạy trên **máy chủ EC2**.
    
    - 54.251.242.155: Là địa chỉ IP công khai của máy chủ EC2.
        
    - :8082: Cổng mà dịch vụ đang lắng nghe.
        
    - /docs: Đường dẫn mặc định của FastAPI để hiển thị giao diện Swagger UI.
        

---

### **🏃🏻 5. Chạy kiểm thử tích hợp (Run Integration test)**

Kiểm thử tích hợp (Integration Test) dùng để kiểm tra xem các thành phần khác nhau của ứng dụng (trong trường hợp này là các API) có hoạt động đúng khi kết hợp với nhau không.

- **Check the TESTING_URL value in test_api.py**: Trước khi chạy kiểm thử, bạn phải mở file test_api.py và chắc chắn rằng biến TESTING_URL được đặt đúng bằng địa chỉ của dịch vụ ML đang chạy (ví dụ: http://54.251.242.155:8082).
    
- **pytest**:
    
    - pytest là một framework kiểm thử phổ biến trong Python.
        
    - Bạn cần đảm bảo môi trường ảo (env) đã được kích hoạt.
        
    - Chạy lệnh pytest trong thư mục gốc của dự án, nó sẽ tự động tìm và thực thi các file kiểm thử (như test_api.py), sau đó báo cáo kết quả thành công hay thất bại.


---


Chắc chắn rồi! Dưới đây là các bước bạn cần làm, được sắp xếp theo đúng thứ tự từ đầu đến cuối. Bạn chỉ cần thực hiện lần lượt các lệnh này.

---

### **Tóm tắt quy trình:**

1. **Chuẩn bị (Trên máy tính cá nhân):** Lấy "chìa khóa" truy cập.
    
2. **Kết nối (Từ máy tính cá nhân):** Truy cập vào máy chủ EC2.
    
3. **Cài đặt (Trên máy chủ EC2):** Tải code và cài đặt các thư viện cần thiết.
    
4. **Chạy (Trên máy chủ EC2):** Khởi động dịch vụ ML.
    
5. **Kiểm tra (Từ máy tính cá nhân):** Xác nhận dịch vụ đang hoạt động.
    

---

### **Bước 0: Chuẩn bị (Thực hiện một lần duy nhất)**

- **Việc cần làm:** Liên hệ **anh HoanVoESTEC** để nhận file privatekey.pem.
    
- **Hành động:** Lưu file này vào một thư mục dễ nhớ trên máy tính của bạn (ví dụ: C:\Users\YourName\ssh_keys\privatekey.pem).
    

### **Bước 1: Kết nối vào máy chủ EC2 (Thực hiện trên máy tính cá nhân)**

Mở terminal trên máy tính của bạn (Command Prompt, PowerShell, VSCode Terminal, hoặc Terminal trên macOS/Linux) và chạy lệnh sau:

Generated bash

```
# Thay "ĐƯỜNG_DẪN_TỚI_FILE/privatekey.pem" bằng đường dẫn thực tế của bạn
ssh -i "ĐƯỜNG_DẪN_TỚI_FILE/privatekey.pem" ubuntu@ec2-54-251-242-155.ap-southeast-1.compute.amazonaws.com
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Bash

- **Ví dụ trên Windows:**  
    ssh -i "C:\Users\YourName\ssh_keys\privatekey.pem" ubuntu@ec2-54-251-242-155.ap-southeast-1.compute.amazonaws.com
    
- **Ví dụ trên macOS/Linux:**  
    ssh -i "~/ssh_keys/privatekey.pem" ubuntu@ec2-54-251-242-155.ap-southeast-1.compute.amazonaws.com
    

**Sau khi chạy lệnh này thành công, bạn đã ở trong terminal của máy chủ EC2.** Tất cả các lệnh ở các bước tiếp theo sẽ được thực hiện tại đây.

### **Bước 2: Tải mã nguồn và cài đặt môi trường (Thực hiện trên máy chủ EC2)**

Chạy lần lượt các lệnh sau trên terminal của EC2:

1. **Tải mã nguồn từ GitHub:**
    
    Generated bash
    
    ```
    git clone https://github.com/estec-digital/ESKilnMaster---BinhPhuoc---ML.git
    ```
    
    Use code [with caution](https://support.google.com/legal/answer/13505487).Bash
    
2. **Di chuyển vào thư mục dự án:**
    
    Generated bash
    
    ```
    cd ESKilnMaster---BinhPhuoc---ML
    ```
    
    Use code [with caution](https://support.google.com/legal/answer/13505487).Bash
    
3. **Tạo môi trường ảo (Nếu chưa có virtualenv, chạy sudo apt update && sudo apt install -y python3-virtualenv):**
    
    Generated bash
    
    ```
    virtualenv env
    ```
    
    Use code [with caution](https://support.google.com/legal/answer/13505487).Bash
    
4. **Kích hoạt môi trường ảo:**
    
    Generated bash
    
    ```
    source env/bin/activate
    ```
    
    Use code [with caution](https://support.google.com/legal/answer/13505487).Bash
    
    (Bạn sẽ thấy (env) xuất hiện ở đầu dòng lệnh).
    
5. **Cài đặt tất cả các thư viện cần thiết:**
    
    Generated bash
    
    ```
    pip install -r requirements.txt
    ```
    
    Use code [with caution](https://support.google.com/legal/answer/13505487).Bash
    
    (Bước này có thể mất vài phút).
    

### **Bước 3: Chạy dịch vụ ML (Thực hiện trên máy chủ EC2)**

Bây giờ, hãy khởi động dịch vụ để nó chạy ở chế độ nền.

Generated bash

```
nohup uvicorn src.main:app --port 8082 --host 0.0.0.0 &
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Bash

- Lệnh này sẽ khởi động dịch vụ trên cổng 8082 và chạy ngầm, kể cả khi bạn đóng terminal.
    
- Bạn sẽ thấy một thông báo như [1] 12345 và nohup: ignoring input and appending output to 'nohup.out'. Điều này là bình thường.
    

### **Bước 4: Kiểm tra xem dịch vụ đã chạy thành công chưa (Thực hiện trên máy tính cá nhân)**

Mở trình duyệt web trên máy tính của bạn và truy cập vào địa chỉ sau:

**[http://54.251.242.155:8082/docs](https://www.google.com/url?sa=E&q=http%3A%2F%2F54.251.242.155%3A8082%2Fdocs)**

Nếu bạn thấy trang **Swagger UI** với danh sách các API hiện ra, nghĩa là bạn đã triển khai thành công!

---

### **Các lệnh quản lý hữu ích (Thực hiện trên máy chủ EC2)**

Bạn cần kết nối lại vào EC2 bằng Bước 1 nếu đã ngắt kết nối.

- **Để kiểm tra xem dịch vụ có đang chạy hay không:**
    
    Generated bash
    
    ```
    ps aux | grep 8082
    ```
    
    Use code [with caution](https://support.google.com/legal/answer/13505487).Bash
    
    Lệnh này sẽ hiển thị thông tin về tiến trình đang chạy trên cổng 8082. Hãy ghi nhớ số **PID** (Process ID) của nó.
    
- **Để dừng dịch vụ:**
    
    Generated bash
    
    ```
    # Thay <SỐ_PID> bằng số bạn tìm được ở trên
    kill -9 <SỐ_PID>
    ```
    
    Use code [with caution](https://support.google.com/legal/answer/13505487).Bash
    
    Ví dụ: kill -9 12345
    
- **Để khởi động lại dịch vụ sau khi đã dừng:**
    
    1. Vào đúng thư mục: cd ESKilnMaster---BinhPhuoc---ML
        
    2. Kích hoạt môi trường ảo: source env/bin/activate
        
    3. Chạy lại lệnh ở **Bước 3**: nohup uvicorn src.main:app --port 8082 --host 0.0.0.0 &