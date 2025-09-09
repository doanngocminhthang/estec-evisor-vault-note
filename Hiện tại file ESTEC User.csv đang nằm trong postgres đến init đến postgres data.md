Chào bạn, vị trí đó chưa chính xác. Việc bạn đặt file vào thư mục con `postgres_data` sẽ khiến script khởi tạo không tìm thấy nó.

Khi Docker chạy, nó sẽ ánh xạ (map) toàn bộ thư mục `postgres/init` từ máy bạn vào thư mục `/docker-entrypoint-initdb.d` bên trong container. Do đó, đường dẫn bên trong container sẽ trở nên phức tạp và không khớp với những gì script `init.sql` đang tìm kiếm.

---

### ## Cách khắc phục đơn giản nhất: Di chuyển file

Bạn chỉ cần di chuyển file `ESTEC-User.csv` ra khỏi thư mục con `postgres_data`.

- **Từ vị trí hiện tại:** `.../postgres/init/postgres_data/ESTEC-User.csv`
    
- **Di chuyển đến vị trí đúng:** `.../postgres/init/ESTEC-User.csv`
    

Nói cách khác, hãy đảm bảo file `ESTEC-User.csv` và file `init.sql` nằm **ngang hàng nhau** bên trong thư mục `postgres/init`.

Bằng cách này, khi container khởi động, cả hai file sẽ cùng nằm trong thư mục `/docker-entrypoint-initdb.d`, và lệnh `COPY` bên trong `init.sql` sẽ tìm thấy file CSV một cách dễ dàng.

---

### ## Các bước tiếp theo

Sau khi đã di chuyển file đến đúng vị trí, bạn hãy chạy lại các lệnh sau để tạo lại database từ đầu:

1. `docker-compose down -v`
    
2. `docker-compose up -d`