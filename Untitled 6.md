Chắc chắn rồi! Viết test cho chức năng đăng nhập là một phần cực kỳ quan trọng. Dưới đây là một file pytest hoàn chỉnh để kiểm thử API /Login của bạn, bao gồm cả các trường hợp thành công, thất bại và lỗi đầu vào.

API này có một sự phụ thuộc lớn là **kết nối cơ sở dữ liệu (database)**. Vì vậy, tôi sẽ trình bày theo 2 cấp độ:

1. **Kiểm thử Tích hợp (Integration Tests):** Cách đơn giản nhất, yêu cầu API phải kết nối được với một database thật (database test).
    
2. **Kiểm thử Đơn vị với Mocking (Unit Tests with Mocking):** Cách nâng cao, cho phép bạn giả lập (mock) kết nối database để kiểm thử logic của API mà không cần database thật.
    

---

### **Cấp độ 1: Kiểm thử Tích hợp (Cách tiếp cận đơn giản nhất)**

Cách này giả định rằng bạn có một database đang chạy để test, và trong đó đã có sẵn một tài khoản người dùng.

#### **Bước 1: Chuẩn bị**

1. Trong môi trường ảo của bạn, hãy cài đặt requests:
    
    Generated bash
    
    ```
    pip install requests
    ```
    
    Use code [with caution](https://support.google.com/legal/answer/13505487).Bash
    
2. Tạo một file mới tên là test_authentication.py.
    
3. Copy và dán toàn bộ code dưới đây vào file đó.
    

#### **Bước 2: Nội dung file test_authentication.py**

Generated python

```
import pytest
import requests

# --- Cấu hình ---
# Địa chỉ của dịch vụ API đang chạy
BASE_URL = "http://127.0.0.1:8082"
API_ENDPOINT = f"{BASE_URL}/Login"

# --- Dữ liệu test ---
# QUAN TRỌNG: Bạn cần đảm bảo tài khoản này tồn tại trong database test của bạn.
VALID_USERNAME = "hoanvlh"
VALID_PASSWORD = "Ef27Xw34" # Mật khẩu đúng
INVALID_PASSWORD = "wrong_password_123" # Mật khẩu sai

# --- Bắt đầu viết Test Cases ---

def test_login_success():
    """
    Ca kiểm thử 1: Đăng nhập thành công (Happy Path)
    - Gửi username và password chính xác.
    - Mong đợi nhận về status code 200 và một phản hồi thành công (ví dụ: chứa token).
    """
    # Arrange: Chuẩn bị dữ liệu
    payload = {
        "username": VALID_USERNAME,
        "password": VALID_PASSWORD
    }

    # Act: Gửi yêu cầu POST
    response = requests.post(API_ENDPOINT, json=payload)

    # Assert: Kiểm tra kết quả
    assert response.status_code == 200, f"Expected 200, got {response.status_code}. Body: {response.text}"
    
    response_data = response.json()
    # Giả định rằng khi thành công, API trả về {"status": "success", ...}
    # Bạn cần thay đổi 'success' nếu logic của bạn trả về khác.
    assert response_data.get("status") == "success", "Login status should be 'success'"
    # Giả định rằng API trả về một 'token' khi đăng nhập thành công
    assert "token" in response_data, "Response should contain a 'token' on successful login"
    
    print(f"\n[Success Login Test] PASSED. Token received.")


def test_login_failed_wrong_password():
    """
    Ca kiểm thử 2: Đăng nhập thất bại do sai mật khẩu
    - Gửi username đúng nhưng password sai.
    - Mong đợi nhận về status code 401 (Unauthorized) hoặc một thông báo lỗi cụ thể.
    """
    # Arrange
    payload = {
        "username": VALID_USERNAME,
        "password": INVALID_PASSWORD
    }

    # Act
    response = requests.post(API_ENDPOINT, json=payload)

    # Assert
    # Một API tốt thường trả về 401 cho lỗi xác thực.
    # Tuy nhiên, nếu API của bạn trả về 200 nhưng với body báo lỗi, hãy sửa lại assert.
    assert response.status_code == 401, f"Expected 401, got {response.status_code}. Body: {response.text}"
    
    response_data = response.json()
    assert response_data.get("status") == "error", "Login status should be 'error' for wrong password"
    assert "Invalid username or password" in response_data.get("message", ""), "Error message is not as expected"
    
    print(f"\n[Wrong Password Test] PASSED. Correctly handled wrong password.")


def test_login_missing_password_field():
    """
    Ca kiểm thử 3: Lỗi xác thực đầu vào - Thiếu trường 'password'
    - Gửi yêu cầu chỉ có username.
    - Mong đợi FastAPI tự động trả về lỗi 422 Unprocessable Entity.
    """
    # Arrange
    payload = {
        "username": VALID_USERNAME
        # Thiếu "password"
    }

    # Act
    response = requests.post(API_ENDPOINT, json=payload)

    # Assert
    assert response.status_code == 422, f"Expected 422, got {response.status_code}"
    
    error_details = response.json().get("detail", [])
    assert error_details[0]["msg"] == "Field required", "Error message should indicate a required field is missing"
    assert error_details[0]["loc"] == ["body", "password"], "Error should be located at the 'password' field"
    
    print(f"\n[Missing Field Test] PASSED. Correctly validated missing password.")
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

---

### **Cấp độ 2: Kiểm thử Đơn vị với Mocking (Nâng cao)**

Cách này rất mạnh mẽ, nó cho phép bạn kiểm tra logic của hàm Authentication_api mà **không cần kết nối database thật**. Bạn sẽ "giả lập" hàm get_postgres_connection và Authentication_function.

#### **Bước 1: Chuẩn bị**

1. Cài đặt thêm pytest-mock:
    
    Generated bash
    
    ```
    pip install pytest-mock
    ```
    
    Use code [with caution](https://support.google.com/legal/answer/13505487).Bash
    
2. Thêm đoạn code sau vào cuối file test_authentication.py.
    

#### **Bước 2: Code kiểm thử với Mocking**

Generated python

```
# --- Code cho Cấp độ 2: Kiểm thử với Mocking ---

def test_login_api_handles_database_exception(mocker):
    """
    Ca kiểm thử 4 (Mocking): Xử lý lỗi khi không kết nối được database
    - Giả lập (mock) hàm 'get_postgres_connection' để nó báo lỗi.
    - Mong đợi API trả về phản hồi lỗi một cách an toàn.
    """
    # Arrange: Giả lập hàm kết nối DB để nó luôn gây ra lỗi Exception
    # THAY 'src.main' bằng đường dẫn đúng đến file chứa hàm của bạn, ví dụ 'app.api.get_postgres_connection'
    mocker.patch('src.main.get_postgres_connection', side_effect=Exception("Cannot connect to DB!"))
    
    payload = {
        "username": VALID_USERNAME,
        "password": VALID_PASSWORD
    }

    # Act
    response = requests.post(API_ENDPOINT, json=payload)

    # Assert
    # Dựa vào code của bạn, khi có exception nó vẫn trả về 200 OK
    assert response.status_code == 200, "API should handle exception gracefully and return 200"
    
    response_data = response.json()
    assert response_data.get("status") == "error", "Status should be 'error' when DB connection fails"
    assert "Cannot connect to DB!" in response_data.get("message", ""), "Error message should reflect the DB connection error"
    
    print(f"\n[DB Exception Mock Test] PASSED. Correctly handled database connection failure.")
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

**Lưu ý quan trọng cho phần Mocking:**

- Dòng mocker.patch('src.main.get_postgres_connection', ...) là quan trọng nhất. Bạn phải thay thế 'src.main.get_postgres_connection' bằng đường dẫn Python tuyệt đối đến nơi bạn định nghĩa hàm get_postgres_connection. Ví dụ, nếu file của bạn là my_app/auth/db.py, đường dẫn sẽ là 'my_app.auth.db.get_postgres_connection'.
    

### **Cách chạy**

1. Đảm bảo dịch vụ API đang chạy.
    
2. Mở terminal, kích hoạt môi trường ảo.
    
3. Chạy lệnh:
    
    Generated bash
    
    ```
    pytest -v test_authentication.py
    ```
    
    Use code [with caution](https://support.google.com/legal/answer/13505487).Bash
    

Bạn sẽ thấy kết quả của từng test case. Cách tiếp cận này giúp bạn cover được cả logic nghiệp vụ (đăng nhập đúng/sai) và các lỗi kỹ thuật (sai đầu vào, lỗi hệ thống), đảm bảo API của bạn cực kỳ vững chắc.