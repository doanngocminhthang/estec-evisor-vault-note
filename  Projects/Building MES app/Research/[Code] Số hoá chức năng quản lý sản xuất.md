Tuyệt vời! Bạn đã hoàn thành xuất sắc giai đoạn đầu tiên và quan trọng nhất. Giao diện của bạn bây giờ đã có thể:

1. **Hiển thị** danh sách các Lệnh Sản Xuất từ backend.
    
2. **Tạo** một Lệnh Sản Xuất mới.
    

Đây chính là nền tảng vững chắc để bạn tiếp tục số hóa các quy trình phức tạp hơn. Nhìn vào yêu cầu của bạn, chúng ta đã hoàn thành phần đầu của mục "Quản lý Lệnh Sản Xuất".

**Yêu cầu của bạn:**

> - **[Xong]** Tạo Lệnh Sản Xuất mới với mã duy nhất, tên dự án, khách hàng, deadline.
>     
> - **[Tiếp theo]** Đính kèm tài liệu kỹ thuật (Bản vẽ, BOQ, Spec) vào từng lệnh.
>     
> - **[Tiếp theo]** Quản lý phiên bản tài liệu (chỉ cho phép sử dụng phiên bản đã được phê duyệt).
>     

Bây giờ, hãy cùng nhau xây dựng các bước tiếp theo để hoàn thiện chức năng quản lý này.

---

### **Lộ Trình Tiếp Theo: "Từ Lệnh Sản Xuất Đến Chi Tiết Công Việc"**

Mục tiêu của giai đoạn này là làm cho mỗi dòng trong bảng của bạn trở nên "sống động". Khi người dùng nhấp vào một Lệnh Sản Xuất, họ phải thấy được toàn bộ chi tiết bên trong nó.

#### **Bước 1: Tạo Trang Chi Tiết Lệnh Sản Xuất (Work Order Detail Page)**

Hiện tại, toàn bộ ứng dụng của bạn chỉ có một trang. Chúng ta cần một hệ thống điều hướng (routing) để có thể chuyển qua lại giữa trang danh sách và trang chi tiết.

- **Công việc Frontend:**
    
    1. **Cài đặt Vue Router:** npm install vue-router.
        
    2. **Cấu hình Vue Router:** Tạo ra hai đường dẫn (routes):
        
        - /: Trang danh sách Lệnh Sản Xuất (trang bạn đang có).
            
        - /work-orders/:id: Trang chi tiết cho một Lệnh Sản Xuất có id cụ thể.
            
    3. **Thiết kế Trang Chi Tiết:** Trang này sẽ hiển thị thông tin chi tiết của dự án và sẽ là nơi chứa các chức năng tiếp theo (đính kèm file, quản lý công đoạn...).
        
    4. **Cập nhật bảng danh sách:** Biến mỗi dòng trong bảng thành một link, khi nhấp vào sẽ điều hướng đến trang chi tiết tương ứng.
        
- **Công việc Backend:**
    
    1. **Tạo API GET /api/work-orders/{id}:** Viết một endpoint mới để trả về thông tin chi tiết của một Lệnh Sản Xuất duy nhất dựa trên ID của nó.
        

#### **Bước 2: Xây Dựng Chức Năng Đính Kèm & Quản Lý Tài Liệu**

Đây là lúc bạn hiện thực hóa yêu cầu "Đính kèm tài liệu kỹ thuật". Chức năng này sẽ nằm trong Trang Chi Tiết Lệnh Sản Xuất.

- **Công việc Backend:**
    
    1. **Sửa Database:**
        
        - Tạo một bảng mới tên là documents với các cột: id, work_order_id (khóa ngoại liên kết tới bảng workorders), file_name, file_path (đường dẫn lưu file trên server), version, status ('Draft', 'Approved'), uploaded_at, uploaded_by.
            
    2. **Chạy Alembic:** Dùng alembic revision --autogenerate và alembic upgrade head để tạo bảng mới này trong database.
        
    3. **Tạo API Upload:**
        
        - Viết một API mới: POST /api/work-orders/{id}/documents. API này sẽ nhận file từ frontend, lưu file vào một thư mục trên server, và tạo một bản ghi mới trong bảng documents.
            
    4. **Tạo API Lấy Danh Sách Tài Liệu:**
        
        - Viết một API mới: GET /api/work-orders/{id}/documents. API này sẽ trả về danh sách tất cả các tài liệu đã được đính kèm cho một Lệnh Sản Xuất.
            
- **Công việc Frontend (trên Trang Chi Tiết):**
    
    1. **Tạo Component Upload:** Sử dụng component <el-upload> của Element Plus để tạo một giao diện cho phép người dùng chọn và tải file lên.
        
    2. **Tạo Component Danh Sách Tài Liệu:** Tạo một cái bảng để hiển thị các file đã upload (tên file, phiên bản, ngày tải lên, nút tải xuống, nút xóa...).
        

#### **Bước 3: Xây Dựng Chức Năng Quản Lý Phiên Bản & Phê Duyệt**

Đây là phần nâng cao của quản lý tài liệu.

- **Công việc Backend:**
    
    1. **API Phê Duyệt:** Tạo một API PUT /api/documents/{doc_id}/approve. API này sẽ chỉ cho phép người có quyền (ví dụ: Trưởng xưởng) gọi đến. Khi được gọi, nó sẽ đổi status của tài liệu trong database thành 'Approved'.
        
    2. **Cập nhật API Lấy Danh Sách:** Sửa lại API GET /api/work-orders/{id}/documents để nó có thể lọc theo status. Ví dụ: GET .../documents?status=Approved sẽ chỉ trả về các file đã được duyệt.
        
- **Công việc Frontend (trên Trang Chi Tiết):**
    
    1. **Hiển thị Trạng thái:** Trong bảng danh sách tài liệu, thêm một cột "Trạng thái" để hiển thị 'Draft' hay 'Approved'.
        
    2. **Thêm Nút Phê Duyệt:** Nếu người dùng đăng nhập có quyền, bên cạnh mỗi tài liệu 'Draft' sẽ có một nút "Phê duyệt". Nhấn nút này sẽ gọi API phê duyệt.
        
    3. **Logic hiển thị:** Đảm bảo rằng ở giao diện dành cho công nhân, họ chỉ có thể thấy và tải về các tài liệu đã được 'Approved'.
        

### **Tóm Tắt Kế Hoạch Hành Động Ngay Bây Giờ**

1. **Tập trung vào Backend trước:** Hoàn thiện API GET /api/work-orders/{id}.
    
2. **Chuyển sang Frontend:** Cài đặt vue-router và tạo ra Trang Chi Tiết Lệnh Sản Xuất, gọi API ở trên để hiển thị dữ liệu.
    
3. **Làm cho bảng danh sách có thể nhấp vào được** để điều hướng đến trang chi tiết.
    

Sau khi hoàn thành 3 việc này, bạn sẽ có một hệ thống hoàn chỉnh cho việc xem danh sách và xem chi tiết. Đó là nền tảng để bạn xây dựng tiếp các tính năng đính kèm file phức tạp hơn.


---


Tuyệt vời! Chúng ta sẽ cùng nhau xây dựng từng bước một theo lộ trình đã đề ra. Tôi sẽ cung cấp code chi tiết cho cả Backend (FastAPI) và Frontend (Vue.js + Element Plus).

Hãy bắt đầu với **"Kế Hoạch Hành Động Ngay Bây Giờ"**.

---

### **Bước 1 & 2: Tạo API Chi Tiết (Backend) và Trang Chi Tiết (Frontend)**

Mục tiêu là khi bạn nhấp vào một Lệnh Sản Xuất trong danh sách, ứng dụng sẽ chuyển sang một trang mới hiển thị đầy đủ thông tin của lệnh đó.

#### **1. Công việc Backend: Tạo API GET /api/work-orders/{id}**

API này sẽ lấy thông tin chi tiết của một Lệnh Sản Xuất dựa trên ID.

**Trong file main.py của bạn, hãy thêm endpoint mới này:**

Generated python

```
# main.py
# ... (giữ nguyên các import hiện có)
from fastapi import FastAPI, Depends, HTTPException, Path # Thêm HTTPException và Path
from sqlalchemy.orm import Session
from typing import List

import models
import schemas
from database import SessionLocal, engine

# ... (giữ nguyên code của bạn)

# --- Endpoint MỚI để lấy chi tiết một Work Order ---
# Đặt nó ngay sau endpoint GET /api/work-orders
@app.get("/api/work-orders/{work_order_id}", response_model=schemas.WorkOrder)
def read_work_order(
    work_order_id: int = Path(..., gt=0, description="ID của Lệnh Sản Xuất cần lấy thông tin"), 
    db: Session = Depends(get_db)
):
    """
    Lấy thông tin chi tiết của một Lệnh Sản Xuất theo ID.
    """
    db_work_order = db.query(models.WorkOrder).filter(models.WorkOrder.id == work_order_id).first()
    if db_work_order is None:
        raise HTTPException(status_code=404, detail="Work Order not found")
    return db_work_order

# ... (giữ nguyên code còn lại)


```
[[[Error] Lỗi NameError name schemas is not defined]]
Use code [with caution](https://support.google.com/legal/answer/13505487).Python

**Giải thích:**

- "/api/work-orders/{work_order_id}": Định nghĩa một đường dẫn động. Bất cứ giá trị nào được đặt ở {work_order_id} sẽ được truyền vào hàm.
    
- work_order_id: int = Path(...): FastAPI sẽ tự động xác thực rằng work_order_id là một số nguyên lớn hơn 0.
    
- db.query(...).filter(...).first(): Truy vấn database để tìm bản ghi có id khớp.
    
- raise HTTPException(status_code=404, ...): Nếu không tìm thấy, trả về lỗi 404 Not Found, đây là một practice tốt cho API.
    

Bây giờ, hãy khởi động lại server FastAPI của bạn. Backend đã sẵn sàng.

#### **2. Công việc Frontend: Cài đặt Vue Router và Tạo Trang Chi Tiết**

**a. Cài đặt Vue Router:**

Mở terminal trong thư mục frontend của bạn và chạy lệnh:

Generated bash

```
npm install vue-router@4
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Bash

(Chúng ta dùng @4 để chắc chắn cài đúng phiên bản cho Vue 3).

**b. Cấu hình Router:**

Tạo một thư mục mới src/router và một file index.js bên trong nó.

**File: src/router/index.js**

Generated javascript

```
import { createRouter, createWebHistory } from 'vue-router';
import WorkOrderList from '../components/WorkOrderList.vue'; // Chúng ta sẽ tạo file này
import WorkOrderDetail from '../components/WorkOrderDetail.vue'; // Và file này

const routes = [
  {
    path: '/',
    name: 'WorkOrderList',
    component: WorkOrderList,
  },
  {
    path: '/work-orders/:id',
    name: 'WorkOrderDetail',
    component: WorkOrderDetail,
    props: true, // Rất quan trọng! Giúp truyền :id như một prop vào component
  },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});

export default router;
```

Use code [with caution](https://support.google.com/legal/answer/13505487).JavaScript

**c. Cập nhật main.js để sử dụng Router:**

**File: src/main.js**

Generated javascript

```
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'
import router from './router' // <--- Import router

const app = createApp(App)

app.use(ElementPlus)
app.use(router) // <--- Sử dụng router
app.mount('#app')
```

Use code [with caution](https://support.google.com/legal/answer/13505487).JavaScript

**d. Tái cấu trúc App.vue và tạo Components mới:**

App.vue bây giờ sẽ là file layout chính, chứa <router-view> để hiển thị các trang. Logic của bảng danh sách sẽ được chuyển vào WorkOrderList.vue.

**File: src/App.vue (Nội dung mới)**

Generated vue

```
<template>
  <el-container style="height: 100vh;">
    <el-header style="text-align: center; font-size: 20px; background-color: #409EFF; color: white; line-height: 60px;">
      Hệ Thống Quản Lý Sản Xuất
    </el-header>
    <el-main>
      <router-view></router-view> <!-- Đây là nơi các trang của bạn sẽ được hiển thị -->
    </el-main>
  </el-container>
</template>

<script setup>
// File này bây giờ rất đơn giản
</script>

<style>
body {
  margin: 0;
}
</style>
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Vue

**Tạo file src/components/WorkOrderList.vue (chứa bảng danh sách):**

Hãy copy toàn bộ code trong <template> và <script setup> từ file App.vue cũ của bạn vào file mới này. Nó sẽ trông như sau:

**File: src/components/WorkOrderList.vue**

Generated vue

```
<template>
  <!-- Toàn bộ code của bảng và form tạo mới được đặt ở đây -->
  <el-button type="primary" @click="dialogVisible = true">Tạo Lệnh Sản Xuất Mới</el-button>

  <!-- Dialog tạo mới -->
  <el-dialog v-model="dialogVisible" title="Tạo Lệnh Sản Xuất Mới" width="500px">
    <!-- ... form của bạn ... -->
  </el-dialog>

  <!-- Bảng danh sách Lệnh Sản Xuất -->
  <el-table :data="workOrders" style="width: 100%; margin-top: 20px" v-loading="loading">
    <el-table-column prop="id" label="ID" width="80" />
    <el-table-column prop="work_order_code" label="Mã Lệnh SX" width="180" />
    <el-table-column prop="project_name" label="Tên Dự Án" />
    <el-table-column prop="customer" label="Khách Hàng" />
    <el-table-column prop="deadline" label="Deadline" />
  </el-table>
</template>

<script setup>
// Toàn bộ logic (ref, onMounted, fetchWorkOrders, createWorkOrder) từ App.vue cũ được đặt ở đây
import { ref, onMounted } from 'vue';
import { ElMessage } from 'element-plus';

const workOrders = ref([]);
const loading = ref(true);
const dialogVisible = ref(false);
const newWorkOrderForm = ref({
  project_name: '',
  customer: '',
  deadline: '',
});

async function fetchWorkOrders() {
  loading.value = true;
  try {
    const response = await fetch('/api/work-orders');
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    workOrders.value = await response.json();
  } catch (error) {
    ElMessage.error('Lỗi khi tải danh sách lệnh sản xuất!');
    console.error(error);
  } finally {
    loading.value = false;
  }
}

async function createWorkOrder() {
  try {
    const response = await fetch('/api/work-orders', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(newWorkOrderForm.value),
    });
    if (!response.ok) {
      throw new Error('Failed to create work order');
    }
    dialogVisible.value = false;
    ElMessage.success('Tạo lệnh sản xuất thành công!');
    fetchWorkOrders(); // Tải lại danh sách
    // Reset form
    newWorkOrderForm.value = { project_name: '', customer: '', deadline: '' };
  } catch (error) {
    ElMessage.error('Lỗi khi tạo lệnh sản xuất!');
    console.error(error);
  }
}

onMounted(fetchWorkOrders);
</script>
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Vue

**Tạo file src/components/WorkOrderDetail.vue (Trang chi tiết):**

Đây là component mới hoàn toàn để hiển thị chi tiết.

**File: src/components/WorkOrderDetail.vue**

Generated vue

```
<template>
  <div>
    <!-- Nút quay lại -->
    <el-page-header @back="goBack" content="Chi Tiết Lệnh Sản Xuất">
    </el-page-header>
    
    <el-divider />

    <div v-if="loading" v-loading="loading" style="height: 200px;"></div>
    
    <div v-else-if="workOrder">
      <el-descriptions :column="2" border>
        <el-descriptions-item label="Mã Lệnh SX">{{ workOrder.work_order_code }}</el-descriptions-item>
        <el-descriptions-item label="ID">{{ workOrder.id }}</el-descriptions-item>
        <el-descriptions-item label="Tên Dự Án">{{ workOrder.project_name }}</el-descriptions-item>
        <el-descriptions-item label="Khách Hàng">{{ workOrder.customer }}</el-descriptions-item>
        <el-descriptions-item label="Deadline">
          <el-tag size="small">{{ workOrder.deadline }}</el-tag>
        </el-descriptions-item>
        <el-descriptions-item label="Ngày tạo">
          {{ new Date(workOrder.created_at).toLocaleString() }}
        </el-descriptions-item>
      </el-descriptions>
    </div>

    <el-empty v-else description="Không tìm thấy Lệnh Sản Xuất"></el-empty>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import { ElMessage } from 'element-plus';

// Nhận `id` từ URL thông qua props đã cấu hình trong router
const props = defineProps({
  id: {
    type: String,
    required: true,
  },
});

const router = useRouter();
const workOrder = ref(null);
const loading = ref(true);

async function fetchWorkOrderDetail() {
  loading.value = true;
  try {
    const response = await fetch(`/api/work-orders/${props.id}`);
    if (response.status === 404) {
      workOrder.value = null; // Setเป็น null nếu không tìm thấy
      throw new Error('Work Order not found');
    }
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    workOrder.value = await response.json();
  } catch (error) {
    console.error(error);
    if (error.message !== 'Work Order not found') {
       ElMessage.error('Lỗi khi tải chi tiết lệnh sản xuất!');
    }
  } finally {
    loading.value = false;
  }
}

function goBack() {
  router.push({ name: 'WorkOrderList' });
}

onMounted(() => {
  fetchWorkOrderDetail();
});
</script>

<style scoped>
.el-page-header {
  margin-bottom: 20px;
}
</style>
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Vue

#### **3. Công việc Frontend: Làm cho Bảng Có Thể Click Được**

Bây giờ, chúng ta sẽ quay lại WorkOrderList.vue và biến cột "Mã Lệnh SX" thành một link để điều hướng.

**Cập nhật file src/components/WorkOrderList.vue:**

Tìm đến phần <el-table-column prop="work_order_code" ... /> và thay thế nó bằng đoạn code sau để sử dụng custom template.

Generated vue

```
<!-- Trong file src/components/WorkOrderList.vue -->
<!-- ... -->
  <el-table :data="workOrders" style="width: 100%; margin-top: 20px" v-loading="loading">
    <el-table-column prop="id" label="ID" width="80" />
    
    <!-- CỘT ĐƯỢC CẬP NHẬT -->
    <el-table-column label="Mã Lệnh SX" width="180">
      <template #default="scope">
        <router-link :to="{ name: 'WorkOrderDetail', params: { id: scope.row.id } }" class="work-order-link">
          {{ scope.row.work_order_code }}
        </router-link>
      </template>
    </el-table-column>
    
    <el-table-column prop="project_name" label="Tên Dự Án" />
    <el-table-column prop="customer" label="Khách Hàng" />
    <el-table-column prop="deadline" label="Deadline" />
  </el-table>
<!-- ... -->
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Vue

Thêm một chút CSS để link trông đẹp hơn.

Generated vue

```
<!-- Ở cuối file src/components/WorkOrderList.vue, thêm thẻ <style> -->
<style scoped>
.work-order-link {
  color: #409EFF;
  text-decoration: none;
}
.work-order-link:hover {
  text-decoration: underline;
}
</style>
```

Use code [with caution](https://support.google.com/legal/answer/13505487).Vue

### **Tổng Kết và Chạy Thử**

Sau khi đã hoàn thành các bước trên:

1. Chạy lại server Backend (FastAPI).
    
2. Chạy lại server Frontend (npm run dev).
    
3. Mở trình duyệt ở http://localhost:5173.
    
4. Bạn sẽ thấy danh sách Lệnh Sản Xuất như cũ.
    
5. **Hãy nhấp vào một "Mã Lệnh SX" bất kỳ trong bảng.**
    
6. Ứng dụng sẽ điều hướng bạn đến URL dạng /work-orders/1 và hiển thị trang chi tiết với đầy đủ thông tin của Lệnh Sản Xuất đó.
    
7. Nhấp vào nút "quay lại" sẽ đưa bạn về trang danh sách.
    

**Chúc mừng!** Bạn đã xây dựng thành công nền tảng điều hướng và xem chi tiết. Đây là một bước tiến lớn, làm cho ứng dụng của bạn có cấu trúc và chuyên nghiệp hơn rất nhiều.

Tiếp theo, chúng ta đã sẵn sàng để xây dựng chức năng **"Đính kèm & Quản lý Tài liệu"** ngay trên trang chi tiết này. Hãy cho tôi biết khi bạn đã sẵn sàng cho bước tiếp theo