Lệnh `COPY` trong PostgreSQL dùng để **sao chép dữ liệu hàng loạt** một cách cực kỳ nhanh chóng giữa một file (như file CSV) và một bảng trong database.

---

### ## Ví dụ Dễ Hiểu 엑셀

Hãy tưởng tượng bạn có một file Excel với 10,000 dòng dữ liệu và bạn muốn đưa nó vào một bảng.

- **Cách chậm (dùng `INSERT`):** Giống như bạn gõ lại hoặc copy-paste từng dòng một. Mất rất nhiều thời gian.
    
- **Cách nhanh (dùng `COPY`):** Giống như bạn dùng chức năng **"Import from CSV"** trong Excel. Nó sẽ đọc toàn bộ file và đổ dữ liệu vào bảng chỉ trong một nốt nhạc.
    

Lệnh `COPY` chính là chức năng "Import" siêu tốc của PostgreSQL.

---

### ## Phân tích Cú pháp Lệnh

Hãy xem lại lệnh `COPY` trong file `init.sql` của bạn:

SQL

```
COPY "User" FROM '/path/to/ESTEC-User.csv' DELIMITER ',' CSV HEADER;
```

- **`COPY "User"`**: Sao chép dữ liệu **VÀO** bảng có tên là `User`.
    
- **`FROM '/path/to/ESTEC-User.csv'`**: Lấy dữ liệu **TỪ** file `ESTEC-User.csv`.
    
- **`DELIMITER ','`**: Báo cho PostgreSQL biết rằng các cột trong file được ngăn cách bởi dấu phẩy (`,`).
    
- **`CSV HEADER`**: Báo cho PostgreSQL rằng dòng đầu tiên của file CSV là **dòng tiêu đề** (tên cột) và hãy bỏ qua nó, không nhập vào database.
    

---

### ## Tại sao lại dùng `COPY`?

- **Tốc độ:** Nhanh hơn lệnh `INSERT` gấp nhiều lần khi cần nhập một lượng lớn dữ liệu.
    
- **Hiệu quả:** Chỉ cần một lệnh duy nhất để nhập hàng ngàn hoặc hàng triệu dòng.
    
- **Tiện lợi:** Rất lý tưởng cho việc khởi tạo database với dữ liệu ban đầu, giống như cách bạn đang làm trong dự án EVisor.