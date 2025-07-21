Dựa vào đoạn backend bạn đưa, bạn cần viết test cho **4 hàm** chính sau:

---

## ✅ 1. `Authentication_function`

### Mục đích:

Kiểm tra **đăng nhập thành công / thất bại**

### Test case nên có:

| Test Case      | Mô tả                                                              |
| -------------- | ------------------------------------------------------------------ |
| ✅ Thành công   | Đúng username + password, trả về `status = success`, có session    |
| ❌ Sai mật khẩu | Đúng username nhưng sai password → `status = error`                |
| ❌ Sai username | Username không tồn tại → `status = error`                          |
| ❌ Exception    | Ví dụ: hỏng DB, nên mock `conn.cursor().execute()` raise exception |

---

## ✅ 2. `check_session`

### Mục đích:

Kiểm tra session còn hạn hay hết hạn

### Test case:

|Test Case|Mô tả|
|---|---|
|✅ Hợp lệ|DB có session, `expires_at > now()` → `True`|
|❌ Hết hạn|DB có session, nhưng `expires_at < now()` → `False`|
|❌ Không tồn tại|Không có session → `False`|

---

## ✅ 3. `Authentication_Logout_function`

### Mục đích:

Xóa session của user

### Test case:

|Test Case|Mô tả|
|---|---|
|✅ Đăng xuất thành công|`DELETE FROM Session` đúng `user_id` → `status = success`|
|❌ Exception|Mock lỗi DB → trả về `status = error`|

---

## ✅ 4. `Authentication_ChangePassword_function`

### Mục đích:

Đổi mật khẩu nếu mật khẩu cũ đúng

### Test case:

|Test Case|Mô tả|
|---|---|
|✅ Thành công|Đúng username + mật khẩu → đổi mật khẩu → `success`|
|❌ Sai mật khẩu cũ|Mật khẩu cũ không khớp → `error`|
|❌ Exception|Ví dụ: DB lỗi → `status = error`|

---

## 📦 Tips

- Nên dùng `unittest.mock` để **mock `conn` và `cursor`**.
    
- Không cần kết nối DB thật trong unit test.
    

---

## ✅ Gợi ý `test_auth.py` đơn giản

```python
from unittest.mock import MagicMock
from yourmodule.auth import Authentication_function

def test_auth_success():
    conn = MagicMock()
    cursor = conn.cursor.return_value
    # Giả lập kết quả SELECT
    cursor.fetchone.return_value = ("hoanvlh", "Ef27Xw34", "avatar.png", "Hoan VLH")

    input = MagicMock(username="hoanvlh", password="Ef27Xw34")
    result = Authentication_function(conn, input)
    
    assert result["status"] == "success"
    assert "session_id" in result
```

---

Nếu bạn cần mình viết sẵn test cho từng hàm cụ thể, gửi thêm:

- tên module file `.py` chứa các hàm
    
- bạn dùng `pytest` hay `unittest`
    

Mình sẽ viết cụ thể từng test case cho bạn.