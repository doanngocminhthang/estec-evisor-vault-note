- test chức năng thuật toán chỉnh sửa file chi tiết sau đó merge vào file tổng hợp trước đó
	tạo các file thành phần đã chỉnh sửa thông tin
	lần lượt merge vào file tổng hợp
	file tổng hợp đuôi 443 đầu tiên

![[ES_20250905_095443.xlsx]]

![[todolist5925.png]]


## Trường hợp 1 : Sửa tên nhân sự
- File thành phần 
	- Sửa Lê Vĩnh Hà -> Nguyễn Văn A
	- task : Lên BOQ 1 
hm : đuôi 157

![[ES_20250905_100157.xlsx]]![[todolist5925-1.png]]![[todolist5925-2.png]]
đã chỉnh sửa file thành phần -> thay đổi tên thành Nguyễn Văn A - task của anh Lê Vĩnh Hà bị xóa -> thêm mới Nguyễn Văn A và task cũ của Lê Vĩnh Hà

Đánh giá : Đúng

## Trường hợp 2 : Sửa mô tả công việc
	
	Nhân sự : Lê Vĩnh Hà
	Mô tả công việc : BOQ 1 -> BOQ 11

![[todolist5925-3.png]]

File sau khi merge : đuôi 305
![[todolist5925-4.png]]
![[todolist5925-5.png]]

So sánh với file tổng hợp đầu tiên

![[todolist5925-6.png]]

Logic : Thay đổi BOQ 1 -> BOQ 11 
	Nhân sự : Lê Vĩnh Hà

Đánh giá : Đúng

## Trường hợp 3 : Sửa thời gian bắt đầu , thời gian kết thúc

file thay đổi thời gian
![[Form mau 1 - suatgbdtgkt.xlsx]]
Thay đổi từ 22->24 thành 24/3/2025 -> 28/3/2025
Nhân sự : Lê Vĩnh Hà,
Task : Lên BOQ 1 - thiết bị Moxa để đáp ứng tiến độ

File thm : đuôi 357
![[ES_20250905_104357.xlsx]]

![[todolist5925-7.png]]

thời gian đã được thay đổi , 24-28/03/2025

Đánh giá : Đúng

## TH4 : sửa nơi làm việc

Sửa nơi làm việc cảu nhân sự Lê Vĩnh Hà
Mô tả công việc : Lên BOQ 1 - thiết bị Moxa đáp ứng tiến độ
Từ S -> V
![[todolist5925-8.png]]


File THM : **ES_20250905_105609**

![[todolist5925-9.png]]

kết quả đã thay đổi từ S -> V

File TH trước đó : 

![[todolist5925-10.png]]

