---
aliases:
  - "Lỗi NameError: name 'schemas' is not defined]]"
tags:
---
![[Lỗi NameError name schemas is not defined.png]]

Chính xác! Lỗi này là do tôi đã sơ suất khi cung cấp đoạn code mà không nhắc lại dòng import cần thiết. Xin lỗi bạn!

Lỗi NameError: name 'schemas' is not defined xảy ra vì Python không biết schemas là gì khi bạn dùng nó trong response_model=schemas.WorkOrder.

[[Lỗi ]]

### **Cách Sửa Lỗi**

Bạn chỉ cần đảm bảo rằng file main.py của bạn đã import module schemas.

Hãy mở file main.py và kiểm tra ở phần đầu file. Nó cần phải có dòng import schemas.

**File main.py của bạn nên trông giống như thế này ở phần đầu:**

Generated python

```
# main.py

from fastapi import FastAPI, Depends, HTTPException, Path
from sqlalchemy.orm import Session
from typing import List

# Đảm bảo các dòng import này tồn tại
import models
import schemas  # <--- HÃY THÊM HOẶC ĐẢM BẢO DÒNG NÀY TỒN TẠI
from database import SessionLocal, engine

# ... (phần code còn lại)
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

Dòng import schemas này sẽ nói cho Python biết rằng schemas là một module mà bạn đã tạo (file schemas.py), và nó có thể tìm thấy lớp WorkOrder Pydantic bên trong đó.

**Để cho chắc chắn, đây là toàn bộ file main.py đã được cập nhật đúng:**

Generated python

```
# main.py
from fastapi import FastAPI, Depends, HTTPException, Path
from sqlalchemy.orm import Session
from typing import List
import uvicorn # Thêm nếu bạn dùng để chạy

# Import các module cục bộ
import models
import schemas
from database import SessionLocal, engine

# Tạo các bảng trong database (chỉ chạy lần đầu)
models.Base.metadata.create_all(bind=engine)

app = FastAPI()

# Dependency để lấy database session
def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

# API để lấy danh sách tất cả Work Orders
@app.get("/api/work-orders", response_model=List[schemas.WorkOrder])
def read_work_orders(skip: int = 0, limit: int = 100, db: Session = Depends(get_db)):
    work_orders = db.query(models.WorkOrder).offset(skip).limit(limit).all()
    return work_orders

# API để tạo một Work Order mới
@app.post("/api/work-orders", response_model=schemas.WorkOrder)
def create_work_order(work_order: schemas.WorkOrderCreate, db: Session = Depends(get_db)):
    new_work_order = models.WorkOrder(**work_order.dict())
    db.add(new_work_order)
    db.commit()
    db.refresh(new_work_order)
    # Tạo mã lệnh sản xuất sau khi có ID
    new_work_order.work_order_code = f"LSX-{new_work_order.id:06d}"
    db.commit()
    db.refresh(new_work_order)
    return new_work_order

# --- Endpoint MỚI để lấy chi tiết một Work Order (ĐÃ SỬA) ---
@app.get("/api/work-orders/{work_order_id}", response_model=schemas.WorkOrder)
def read_work_order(
    work_order_id: int = Path(..., gt=0, description="ID của Lệnh Sản Xuất cần lấy thông tin"), 
    db: Session = Depends(get_db)
):
    db_work_order = db.query(models.WorkOrder).filter(models.WorkOrder.id == work_order_id).first()
    if db_work_order is None:
        raise HTTPException(status_code=404, detail="Work Order not found")
    return db_work_order

# Dùng để chạy app với `python main.py`
if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000)
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Python

Bạn chỉ cần thêm dòng import schemas vào đầu file main.py, lưu lại và khởi động lại server FastAPI. Lỗi sẽ được khắc phục.

Sau khi sửa lỗi này, bạn có thể tiếp tục với phần frontend. Tôi đang chờ bạn ở bước tiếp theo