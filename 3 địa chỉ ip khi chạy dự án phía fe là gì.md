```
  VITE v6.3.5  ready in 686 ms

  ➜  Local:   http://localhost:5173/

  ➜  Network: http://192.168.54.152:5173/

  ➜  Network: http://172.22.176.1:5173/

3 địa chỉ ip khi chạy dự án phía frontend là gì
```

Đây là 3 địa chỉ khác nhau để truy cập vào **cùng một** server phát triển frontend của bạn, mỗi địa chỉ dành cho một mục đích riêng.

---

### ## 1. `http://localhost:5173/` (Địa chỉ Local) 💻

- **Ý nghĩa:** `localhost` (hoặc `127.0.0.1`) là một tên đặc biệt, luôn luôn chỉ về **chính chiếc máy tính bạn đang dùng**.
    
- **Ai có thể truy cập?** Chỉ có bạn, trên chính chiếc máy tính đang chạy dự án.
    
- **Khi nào dùng?** Đây là địa chỉ chính mà bạn sẽ sử dụng trong quá trình code và kiểm thử trên máy của mình.
    

---

### ## 2. `http://192.168.54.152:5173/` (Địa chỉ Mạng Nội bộ) 📶

- **Ý nghĩa:** Đây là địa chỉ IP của máy tính bạn trong **mạng nội bộ (LAN)**, ví dụ như mạng Wi-Fi ở công ty hoặc ở nhà.
    
- **Ai có thể truy cập?** Bất kỳ ai khác đang kết nối vào **cùng một mạng Wi-Fi** với bạn.
    
- **Khi nào dùng?** Rất hữu ích khi bạn muốn:
    
    - Cho đồng nghiệp ngồi bên cạnh xem trực tiếp sản phẩm của bạn.
        
    - Kiểm tra trang web trên các thiết bị khác (như điện thoại, máy tính bảng) bằng cách nhập địa chỉ này vào trình duyệt của thiết bị đó.
        

---

### ## 3. `http://172.22.176.1:5173/` (Địa chỉ Mạng khác) 🌐

- **Ý nghĩa:** Đây cũng là một địa chỉ IP khác của máy tính bạn, nhưng trên một **mạng ảo hoặc mạng đặc biệt khác**.
    
- **Nguyên nhân thường gặp:**
    
    - Bạn đang kết nối với một **VPN**.
        
    - Bạn đang sử dụng phần mềm ảo hóa như **Docker** hoặc máy ảo (Virtual Machine), chúng thường tạo ra các mạng ảo riêng.
        
- **Khi nào dùng?** Ít phổ biến hơn, chủ yếu dùng khi cần kết nối giữa các máy trong cùng một mạng ảo đó.
    

---

### ## Tóm tắt

| Địa chỉ                   | Ai có thể truy cập?             | Khi nào dùng?                                     |
| ------------------------- | ------------------------------- | ------------------------------------------------- |
| **`localhost:5173`**      | Chỉ bạn                         | Để code và kiểm thử một mình.                     |
| **`192.168.54.152:5173`** | Mọi người trong cùng mạng Wi-Fi | Để cho đồng nghiệp xem hoặc test trên điện thoại. |
| **`172.22.176.1:5173`**   | Thiết bị trong mạng ảo/VPN      | Dùng cho các trường hợp kết nối mạng đặc biệt.    |