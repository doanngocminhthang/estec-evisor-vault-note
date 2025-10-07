### ## Kế hoạch kiểm thử các API Kho (Warehouse)

| Nhóm API      | Endpoint       | Mục tiêu kiểm thử                          | Dữ liệu đầu vào (Body) ví dụ                           | Kết quả mong đợi (Status Code) |
| ------------- | -------------- | ------------------------------------------ | ------------------------------------------------------ | ------------------------------ |
| **Thống kê**  | `_View`        | Lấy dữ liệu thống kê thành công.           | `{ "fromDate": "2025-10-01", "toDate": "2025-10-07" }` | `200 OK`                       |
|               | `_View_Detail` | Lấy dữ liệu chi tiết của một mục thống kê. | `{ "recordId": 123 }`                                  | `200 OK`                       |
|               | `_DML`         | Thêm/sửa/xóa một bản ghi thống kê.         | `{ "action": "insert", "data": { ... } }`              | `201 Created` / `200 OK`       |
|               | `_Upload`      | Tải lên file dữ liệu thống kê.             | (Form-data với file đính kèm)                          | `200 OK`                       |
| **Xuất/Nhập** | `_View`        | Xem lịch sử xuất/nhập kho.                 | `{ "type": "import", "fromDate": "2025-10-01" }`       | `200 OK`                       |
|               | `_View_Detail` | Xem chi tiết một phiếu xuất/nhập.          | `{ "importExportId": "PNK0045" }`                      | `200 OK`                       |
|               | `_DML`         | Tạo phiếu xuất/nhập kho.                   | `{ "action": "create_import", "data": { ... } }`       | `201 Created`                  |
|               | `_Upload`      | Tải lên file đính kèm cho phiếu.           | (Form-data với file và ID phiếu)                       | `200 OK`                       |


1. Nhóm API Thống kê (WarehouseStatistical)
	1. View...View Detail
		1. thành công
		2. dữ liệu trống
		3. sai tham số
	2. DML
		1. Insert
		2. Update
		3. Delete
		4. Thiếu dữ liệu
	3. Upload 
		1. Test thành công
		2. Test sai định dạng
		3. Test file quá lớn

2. Nhóm API Xuất / Nhập Kho
	1. Xử lý xuất nhập hàng hóa
		1. View và View detail
			1. Test thành công
			2. Test chi tiết
		2. .... DML
			1. Test tạo phiếu nhập
			2. Test tạo phiếu xuất
			3. Test tạo nghiệp vụ không hợp lệ
		3. .... Upload
			1. Test thành công