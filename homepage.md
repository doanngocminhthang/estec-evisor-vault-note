---
tags:
  - ghim
  - tong-quan
  - trang-chu
---
- [[test chức năng thuật toán chỉnh sửa file chi tiết sau đó merge vào file tổng hợp trước đó]]
- - [[Nghiên cứu ứng dụng evisor]]
- [[Set up dự án evisor]]
- [[test chức năng dự án]]
- [[ vẽ workflow evisor cho tài liệu]]
- [[nghiên cứu tài liệu nhôm daknong]]
- [[nghiên cứu lại yêu cầu của evisor từ feedback của anh Hướng]]

Họp 
- 031025
	- ghi chú
		- Sửa mã dự án tổng -> merge vẫn bị lỗi 
		- Chức năng delete file tổng, 
		- Phát triển chức năng group trong excel 
		- Phát triển bút xóa theo mã dự án, 
		- Chức năng xóa file tổng
	- => thêm các TC mới vào file TC để sau này test các chức năng anh em mới phát triển

Test các chức năng mới
 - Xóa các bản ghi công việc dựa theo người thực hiện, mã dự án 
	 - [[xóa người thực hiện]]
		 - [[Excalidraw/xóa người thực hiện|xóa người thực hiện]]
 - Xóa nhiều bản ghi cùng lúc
 - Bộ lọc cho phép chọn khoảng thời gian cụ thê

Tài khoản Evisor  
	username: hoanvlh
	password: example= Ef27Xw34

071025
- Test API cho Kiệt
	- [[test api cho kiệt]]
	- ![[Pasted Image 20251006160906_055.png]]
	- test plan
		- [[tp api]]
	- file upload :
		- ![[homepage.png]]
		- "D:\estec\project\estec_evisor\estec_evisor_research\file upload test cho Kiet\export.xlsx"

101025
- Họp
	- Nhìn vào bảng để xác định các khoảng trống 
		- xanh là ít
		- vàng đỏ còn nhiều
		- tổng hợp lê hoàng ngày 0306 bao nhiêu giờ, có bị đỏ hay không
		- sheet tổng hợp -> sheet chi tiết , tổng hợp thời gian của từng bạn
		- khi nào update file quản lý dự án?? Trưởng ban giám đốc 
		- Nếu thay đổi thời gian thực hiện phải trao đổi PM hoặc ban quản lý dự án
		- Thêm ngày kết thúc mới, thêm thay đổi giao diện  cho ngày kết thúc mới để người PM nhìn vào biết lý do vì sao người thực hiện phải thay đổi ngày kết thúc công việc

Phát triển chức năng người dùng chỉnh sửa thông tin trong file tổng hợp
- Người dùng upload file tổng
- Sau đó người dùng cần chỉnh sửa 1 trong các thông tin trong file tổng
- Khi người dùng thay đổi thông tin cần cập nhật version trong file excel
- Upload lên web, web gửi vào DB
- DB so sánh xem người dùng đã chỉnh sửa trong cột nào
	- 3 cột đầu thì tạo task mới và thay đổi giá trị version
	- các cột còn lại thì thay đổi trạng thái thành đã chỉnh sửa và thay đổi giá trị version

30102025
	Task check chức năng người dùng chỉnh sửa thông tin trong file tổng hợp
	- link check