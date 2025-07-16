Chắc chắn rồi! Với vai trò là một tester, việc hiểu rõ file main.py là cực kỳ quan trọng vì đây chính là "trái tim" của toàn bộ backend, là nơi định nghĩa tất cả các "cánh cửa" (API endpoints) mà hệ thống mở ra cho bên ngoài.

Dưới đây là một bản phân tích chi tiết file main.py này, được trình bày theo góc nhìn của một tester.

---

### **A. Tổng quan và Cấu trúc**

File này có 4 nhiệm vụ chính:

1. **Thiết lập Môi trường:** Tải các biến môi trường (như mật khẩu database, địa chỉ server) từ file .env.
    
2. **Khởi tạo Kết nối:** Tạo các "client" để sẵn sàng kết nối đến hai dịch vụ ngoài quan trọng là **MinIO** (lưu trữ file) và **PostgreSQL** (cơ sở dữ liệu).
    
3. **Định nghĩa Cấu trúc Dữ liệu:** Sử dụng Pydantic để định nghĩa rõ ràng dữ liệu đầu vào (input) cho mỗi API. Đây là "hợp đồng" mà API yêu cầu người gọi phải tuân thủ.
    
4. **Định nghĩa các API Endpoints:** Tạo ra các đường dẫn (URL) mà frontend hoặc tester có thể gọi đến, ví dụ: /Login, /POD_TimeTracker_Upload.
    

---

### **B. Phân tích chi tiết theo từng Nhóm API**

Các API được nhóm lại bằng tags (ví dụ: tags=["POD"], tags=["Authentication"]). Đây là một cách tổ chức rất tốt.

#### **I. Nhóm Authentication (Xác thực người dùng)**

Đây là nhóm API nền tảng, vì hầu hết các API khác đều yêu cầu người dùng phải đăng nhập.

**1. POST /Login**

- **Mục đích:** Cho phép người dùng đăng nhập vào hệ thống.
    
- **Đầu vào (Authentication class):** username (string), password (string).
    
- **Logic chính:**
    
    1. Kết nối đến database PostgreSQL.
        
    2. Gọi hàm Authentication_function() (logic chi tiết nằm trong file Authentication.py) để kiểm tra username và password với dữ liệu trong DB.
        
- **Điểm cần lưu ý cho Tester:**
    
    - **Happy Path:** Test với tài khoản/mật khẩu đúng. Kết quả trả về là gì? (Thường là một token và status "success").
        
    - **Unhappy Path:**
        
        - Test với username sai.
            
        - Test với username đúng nhưng password sai.
            
        - Test với username/password rỗng.
            
        - Test khi database không thể kết nối. API có trả về lỗi "sạch" không? (Nhờ có try...except).
            

**2. POST /Logout**

- **Mục đích:** Đăng xuất người dùng.
    
- **Đầu vào (Authentication_Logout class):** username (string).
    
- **Logic chính:** Gọi hàm Authentication_Logout_function() để có thể là xóa session/token của người dùng khỏi DB.
    
- **Điểm cần lưu ý cho Tester:**
    
    - Làm sao để biết đăng xuất thành công? Bạn phải thực hiện một chuỗi test:
        
        1. Login thành công.
            
        2. Gọi một API yêu cầu xác thực (ví dụ: /POD_TimeTracker_Getfile) -> Thành công.
            
        3. Gọi API /Logout.
            
        4. Gọi lại API /POD_TimeTracker_Getfile một lần nữa -> **Phải thất bại** với lỗi "Phiên làm việc đã hết hạn...".
            

**3. POST /ChangePassword**

- **Mục đích:** Cho phép người dùng đổi mật khẩu.
    
- **Đầu vào (Authentication_ChangePassword class):** username, password (mật khẩu cũ), newpassword.
    
- **Logic chính:** Gọi hàm Authentication_ChangePassword_function() để xác thực mật khẩu cũ trước khi cập nhật mật khẩu mới.
    
- **Điểm cần lưu ý cho Tester:**
    
    - Test trường hợp đổi mật khẩu thành công.
        
    - Test với mật khẩu cũ không chính xác.
        
    - Test với newpassword không hợp lệ (nếu có quy tắc về độ dài, ký tự đặc biệt...).
        

---

#### **II. Nhóm POD (Chức năng nghiệp vụ TimeTracker)**

Đây là nhóm API chính của ứng dụng, và hầu hết đều có một bước kiểm tra chung rất quan trọng: check_session(conn, input.user_id).

**1. POST /POD_TimeTracker_Upload**

- **Mục đích:** Cho phép người dùng tải lên các file Excel.
    
- **Đầu vào:** Không phải là JSON! Đây là List[UploadFile], nghĩa là nó nhận dữ liệu dạng multipart/form-data (dạng form upload file trên web).
    
- **Logic chính:**
    
    1. Lặp qua từng file được gửi lên.
        
    2. Đọc nội dung file.
        
    3. Lưu file lên **MinIO** với một đường dẫn cụ thể.
        
    4. Kiểm tra xem file đó có phải là file summary không bằng hàm issummary_file().
        
    5. Trả về danh sách các đường dẫn file đã upload.
        
- **Điểm cần lưu ý cho Tester:**
    
    - **API này KHÔNG kiểm tra session!** Đây có thể là một điểm cần làm rõ với đội phát triển. Bất kỳ ai cũng có thể upload file?
        
    - Test upload 1 file, nhiều file.
        
    - Test upload file có tên chứa ký tự đặc biệt, tiếng Việt.
        
    - Test upload file rất lớn (kiểm tra giới hạn dung lượng).
        
    - Test upload file không phải là Excel (.txt, .jpg...). API xử lý thế nào?
        
    - Test khi MinIO không thể kết nối.
        

**2. POST /POD_TimeTracker_Merge**

- **Mục đích:** Yêu cầu backend xử lý (gộp) các file Excel đã được upload trước đó.
    
- **Đầu vào (POD_TimeTracker_Merge class):** user_id, path_files (danh sách các đường dẫn file trên MinIO), summary_file (tùy chọn).
    
- **Logic chính:**
    
    1. **Kiểm tra session:** Bước cực kỳ quan trọng. Nếu session không hợp lệ, trả về lỗi ngay.
        
    2. **Rẽ nhánh logic:** Dựa vào việc summary_file có được cung cấp hay không (is None), nó sẽ gọi 1 trong 2 hàm xử lý khác nhau: POD_TimeTracker_Merge_function hoặc POD_TimeTracker_Merge_Manual_function.
        
- **Điểm cần lưu ý cho Tester:**
    
    - Bạn phải cover cả 2 nhánh logic:
        
        - **Ca 1:** Gọi API với summary_file là null hoặc không có.
            
        - **Ca 2:** Gọi API với summary_file có giá trị là một đường dẫn.
            
    - Test với session không hợp lệ.
        
    - Test với path_files chứa đường dẫn đến file không tồn tại trên MinIO.
        

**3. POST /POD_TimeTracker_Getfile & POST /POD_TimeTracker_Download**

- **Mục đích:** Lấy nội dung hoặc tải về một file đã được xử lý từ MinIO.
    
- **Đầu vào:** user_id, path_file (đường dẫn file cần lấy).
    
- **Logic chính:**
    
    1. Kiểm tra session.
        
    2. Gọi hàm tương ứng (_Getfile_function hoặc _Download_function) để lấy file từ MinIO.
        
- **Điểm cần lưu ý cho Tester:**
    
    - Test với session không hợp lệ.
        
    - Test với path_file trỏ đến một file không tồn tại. API trả về lỗi gì?
        
    - Hàm Download có thể sẽ trả về một file stream. Bạn cần kiểm tra Content-Type và Content-Disposition trong header của response để đảm bảo trình duyệt sẽ tự động tải file về.
        

---

### **C. Chiến lược Kiểm thử Tổng thể cho Tester**

1. **Thiết lập môi trường:** Bạn cần một file .env với đầy đủ thông tin để kết nối đến MinIO và PostgreSQL đang chạy (thường là qua Docker).
    
2. **Kiểm tra luồng xác thực (Authentication Flow):** Đây là luồng quan trọng nhất. Phải test Login -> Sử dụng các API POD -> Logout như một chuỗi hoàn chỉnh.
    
3. **Kiểm tra luồng nghiệp vụ (Business Flow):** Upload -> Merge -> Getfile/Download.
    
4. **Tập trung vào các điều kiện rẽ nhánh:** Bất cứ đâu có if/else, bạn cần tạo ít nhất 2 test case để đi vào cả 2 nhánh.
    
5. **Kiểm tra xử lý lỗi:** Cố tình tạo ra các lỗi (session hết hạn, file không tồn tại, database sập...) để xem API có trả về thông báo lỗi thân thiện và an toàn không, thay vì bị crash.
    
6. **Xác thực đầu vào:** Dù FastAPI đã tự động kiểm tra, bạn vẫn nên viết test cho các trường hợp thiếu trường, sai kiểu dữ liệu để đảm bảo API hoạt động đúng như tài liệu.


# Code
```python
from fastapi import FastAPI, UploadFile, File

from pydantic import BaseModel, Field

from minio import Minio

import pandas as pd

from io import BytesIO

from dotenv import load_dotenv

import os

from typing import List, Optional

from datetime import datetime

from src.POD_TimeTracker import *

from src.Authentication import *

from src.DB_Connection import *

import uuid

from fastapi.middleware.cors import CORSMiddleware

  

# Tải biến môi trường từ file .env

load_dotenv()

MINIO_ENDPOINT = os.getenv("MINIO_ENDPOINT")

MINIO_SERVER = os.getenv("MINIO_SERVER")

MINIO_PORT_API_EXTERNAL = os.getenv("MINIO_PORT_API_EXTERNAL")

MINIO_ROOT_USER = os.getenv("MINIO_ROOT_USER")

MINIO_ROOT_PASSWORD = os.getenv("MINIO_ROOT_PASSWORD")

MINIO_BUCKET = os.getenv("MINIO_BUCKET")

  

POSTGRESQL_SERVER = os.getenv("POSTGRESQL_SERVER")

POSTGRES_PORT_EXTERNAL = os.getenv("POSTGRES_PORT_EXTERNAL")

POSTGRES_DB = os.getenv("POSTGRES_DB")

POSTGRES_USER = os.getenv("POSTGRES_USER")

POSTGRES_PASSWORD = os.getenv("POSTGRES_PASSWORD")

  

app = FastAPI()

app.add_middleware(

    CORSMiddleware,

    allow_origins=["*"],

    allow_credentials=True,

    allow_methods=["*"],

    allow_headers=["*"],

)

@app.get("/", tags=["Greeting"])

def read_root():

    return {"message": "Xin chào đây là API của EVisor!"}

  

# Cấu hình MinIO client

minio_client = Minio(

    endpoint=f"{MINIO_SERVER}:{MINIO_PORT_API_EXTERNAL}",

    access_key=f"{MINIO_ROOT_USER}",

    secret_key=f"{MINIO_ROOT_PASSWORD}",

    secure=False

)

print(minio_client)

  

postgres_db = {

    "host": POSTGRESQL_SERVER,

    "port": POSTGRES_PORT_EXTERNAL,

    "database": POSTGRES_DB,

    "user": POSTGRES_USER,

    "password": POSTGRES_PASSWORD

}

  

### POD ###

## TimeTracker

class POD_TimeTracker_Merge(BaseModel):

    request_id: str = Field(default="evisor-1234567890", example="evisor-1234567890")

    user_id: str = Field(default="hoanvlh", example="hoanvlh")

    start_time: datetime = Field(example="2025-06-23T15:20:00")

    path_files: List[str] = Field(example=["data/POD/TimeTracker/Input/Form mau 1.xlsx", "data/POD/TimeTracker/Input/Form mau 2.xlsx"])

    summary_file: Optional[str] = Field(default=None, example="data/POD/TimeTracker/Output/ES_20250704_104529.xlsx")

  

@app.post("/POD_TimeTracker_Merge", tags=["POD"])

def POD_TimeTracker_Merge_api(input: POD_TimeTracker_Merge):

    try:

        conn = get_postgres_connection(POSTGRESQL_SERVER, POSTGRES_PORT_EXTERNAL, POSTGRES_DB, POSTGRES_USER, POSTGRES_PASSWORD)

        session = check_session(conn, input.user_id)

        if not session:

            return {

                "status": "error",

                "message": "Phiên làm việc đã hết hạn hoặc không hợp lệ. Vui lòng đăng nhập lại."

                }

        else:

            if input.summary_file is None:

                return POD_TimeTracker_Merge_function(minio_client, input)

            else:

                return POD_TimeTracker_Merge_Manual_function(minio_client, input)

    except Exception as e:

        return {

            "status": "error",

            "message": str(e)

            }

  

@app.post("/POD_TimeTracker_Upload", tags=["POD"])

async def POD_TimeTracker_Upload_api(files: List[UploadFile] = File(...)):

    try:

        uploaded_paths = []

        summary_file = ''

        for file in files:

            object_name = f"data/POD/TimeTracker/Input/{file.filename}"

            content = await file.read()

            minio_client.put_object(

                MINIO_BUCKET,

                object_name,

                BytesIO(content),

                length=len(content),

                content_type=file.content_type

            )

            issummary = issummary_file(content)

            if issummary:

                summary_file = object_name

            else:

                uploaded_paths.append(object_name)

        return {

            "status": "success",

            "path_files": uploaded_paths,

            "summary_file": summary_file

        }

    except Exception as e:

        return {

            "status": "error",

            "message": str(e)

        }

class POD_TimeTracker_Getfile(BaseModel):

    request_id: str = Field(default="evisor-1234567890", example="evisor-1234567890")

    user_id: str = Field(default="hoanvlh", example="hoanvlh")

    path_file: str = Field(default=None, example="data/POD/TimeTracker/Output/ES_20250702_093042.xlsx")

  

@app.post("/POD_TimeTracker_Getfile", tags=["POD"])

async def POD_TimeTracker_Getfile_postapi(input: POD_TimeTracker_Getfile):

    try:

        conn = get_postgres_connection(POSTGRESQL_SERVER, POSTGRES_PORT_EXTERNAL, POSTGRES_DB, POSTGRES_USER, POSTGRES_PASSWORD)

        session = check_session(conn, input.user_id)

        if not session:

            return {

                "status": "error",

                "message": "Phiên làm việc đã hết hạn hoặc không hợp lệ. Vui lòng đăng nhập lại."

                }

        else:

            return POD_TimeTracker_Getfile_function(minio_client, input, MINIO_BUCKET)

    except Exception as e:

        return {

            "status": "error",

            "message": str(e)

            }

class POD_TimeTracker_Download(BaseModel):

    request_id: str = Field(default="evisor-1234567890", example="evisor-1234567890")

    user_id: str = Field(default="hoanvlh", example="hoanvlh")

    path_file: str = Field(default=None, example="data/POD/TimeTracker/Output/ES_20250702_093042.xlsx")

  

@app.post("/POD_TimeTracker_Download", tags=["POD"])

def POD_TimeTracker_Download_postapi(input: POD_TimeTracker_Download):

    try:

        conn = get_postgres_connection(POSTGRESQL_SERVER, POSTGRES_PORT_EXTERNAL, POSTGRES_DB, POSTGRES_USER, POSTGRES_PASSWORD)

        session = check_session(conn, input.user_id)

  

        if not session:

            return {

                "status": "error",

                "message": "Phiên làm việc đã hết hạn hoặc không hợp lệ. Vui lòng đăng nhập lại."

                }

        else:

            return POD_TimeTracker_Download_function(minio_client, input, MINIO_BUCKET)

    except Exception as e:

        return {

            "status": "error",

            "message": str(e)

            }

### Authentication

class Authentication(BaseModel):

    username: str = Field(example="hoanvlh")

    password: str = Field(example="Ef27Xw34")

  

@app.post("/Login", tags=["Authentication"])

def Authentication_api(input: Authentication):

    try:

        conn = get_postgres_connection(POSTGRESQL_SERVER, POSTGRES_PORT_EXTERNAL, POSTGRES_DB, POSTGRES_USER, POSTGRES_PASSWORD)

        print(f"Connected to PostgreSQL database: {conn}")

        return Authentication_function(conn, input)

    except Exception as e:

        return {

            "status": "error",

            "message": str(e)

            }

  

class Authentication_Logout(BaseModel):

    username: str = Field(example="hoanvlh")

  

@app.post("/Logout", tags=["Authentication"])

def Authentication_Logout_api(input: Authentication_Logout):

    try:

        conn = get_postgres_connection(POSTGRESQL_SERVER, POSTGRES_PORT_EXTERNAL, POSTGRES_DB, POSTGRES_USER, POSTGRES_PASSWORD)

        print(f"Connected to PostgreSQL database: {conn}")

        return Authentication_Logout_function(conn, input)

    except Exception as e:

        return {

            "status": "error",

            "message": str(e)

            }

  

class Authentication_ChangePassword(BaseModel):

    username: str = Field(example="hoanvlh")

    password: str = Field(example="Ef27Xw34")

    newpassword: str = Field(example="123456")

  

@app.post("/ChangePassword", tags=["Authentication"])

def Authentication_ChangePassword_api(input: Authentication_ChangePassword):

    try:

        conn = get_postgres_connection(POSTGRESQL_SERVER, POSTGRES_PORT_EXTERNAL, POSTGRES_DB, POSTGRES_USER, POSTGRES_PASSWORD)

        print(f"Connected to PostgreSQL database: {conn}")

        return Authentication_ChangePassword_function(conn, input)

    except Exception as e:

        return {

            "status": "error",

            "message": str(e)

            }
```
