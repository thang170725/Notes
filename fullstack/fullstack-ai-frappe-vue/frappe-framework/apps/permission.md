PERMISSION (PHÂN QUYỀN) TRONG FRAPPE

Không code. Không lý thuyết hàn lâm.
Chỉ hiểu vì sao ERP sống được là nhờ cái này.

1️⃣ PERMISSION LÀ GÌ? (NÓI 1 CÂU)

Permission = ai được làm gì với Document nào

2️⃣ VÌ SAO PHẢI CÓ PERMISSION?

Ví dụ đời thật:

Người	Có được làm gì?
Nhân viên	Tạo đơn
Quản lý	Duyệt
Kế toán	Xem
Người lạ	Không thấy

👉 Nếu ai cũng sửa được → ERP vô nghĩa.

3️⃣ 3 THỨ CỐT LÕI TRONG PERMISSION
🧩 1. User (Người dùng)

Email login

Có thể có nhiều Role

🧩 2. Role (Vai trò)

Ví dụ:

Librarian

Library Member

System Manager

👉 Role = cái mũ đội trên đầu

🧩 3. Permission Rule

Quy định:

Role nào

Được làm gì (Read / Write / Create / Delete / Submit)

4️⃣ PERMISSION GẮN Ở ĐÂU?

👉 Gắn vào DocType, không gắn vào User.

DocType Article
 ├─ Librarian → full quyền
 └─ Member → chỉ Read


User chỉ việc:

User → có Role → hưởng quyền

5️⃣ CÁC QUYỀN CƠ BẢN (RẤT QUAN TRỌNG)
Quyền	Ý nghĩa
Read	Xem
Write	Sửa
Create	Tạo
Delete	Xóa
Submit	Submit
Cancel	Cancel
Amend	Tạo bản sửa

👉 Không có quyền → nút biến mất

6️⃣ FRAPPE KIỂM TRA PERMISSION KHI NÀO?

Luôn luôn:

Mở List

Mở Form

Save

Submit

Gọi API

👉 Không có chuyện lách UI

7️⃣ THỰC HÀNH NHẸ (RẤT QUAN TRỌNG)
🎯 Mục tiêu

Cảm nhận Permission bằng mắt

BƯỚC 1: Tạo Role

Awesomebar → Role List

New → Article Viewer

BƯỚC 2: Gán Permission cho DocType Article

Mở DocType Article

Phần Permissions

Thêm dòng:

Role: Article Viewer

Tick: Read

Bỏ hết cái khác

Save

BƯỚC 3: Tạo User test

Awesomebar → User List

New User

Gán Role: Article Viewer

Lưu

BƯỚC 4: Login user đó

👉 Bạn sẽ thấy:

Chỉ xem được Article

Không tạo

Không sửa

8️⃣ ĐIỀU CỰC KỲ QUAN TRỌNG

Permission trong Frappe không phải trang trí UI
Nó là security thật

Backend cũng tuân theo rule này.

9️⃣ TÓM TẮT ĐẾN GIỜ

Bạn đã nắm:

DocType = bản thiết kế

Document = dữ liệu thật

Permission = luật chơi

👉 Đây là 3 trụ cột của Frappe.

🔜 PHẦN TIẾP THEO (BẮT ĐẦU THÚ VỊ)
👉 FORM BEHAVIOR (HÀNH VI FORM)

Vì sao đổi Status → field khác bị khóa?

Vì sao có field chỉ đọc?

Logic UI đến từ đâu?

Không code trước, chỉ hiểu.