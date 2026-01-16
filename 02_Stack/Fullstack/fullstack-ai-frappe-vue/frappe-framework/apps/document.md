DOCUMENT LÀ GÌ?
Nói 1 câu:

Document = 1 instance (1 dòng dữ liệu) của DocType

Ví dụ:

DocType: Article
Bạn bấm New và nhập:

Article Name: AI là gì

Author: Thắng

Status: Available

👉 Cái bạn vừa lưu = 1 Document

Nếu bạn tạo 100 bài viết →
100 Document cùng chung 1 DocType

2️⃣ DOC TYPE vs DOCUMENT (PHẢI PHÂN BIỆT RÕ)
DocType	Document
Bản thiết kế	Dữ liệu thật
Tạo 1 lần	Tạo nhiều lần
Dev định nghĩa	User sử dụng
Giống class	Giống object

👉 Không phân biệt được cái này → học Frappe rất mệt

3️⃣ CRUD TRONG FRAPPE DIỄN RA Ở ĐÂU?
C = Create

Bấm New

Lưu form

R = Read

Article List

Mở 1 Article

U = Update

Edit

Save

D = Delete

Delete (nếu có quyền)

👉 Không cần code → Frappe lo hết

4️⃣ NAME – THỨ KHIẾN NHIỀU NGƯỜI RỐI
name là gì?

Là Primary Key

Không nhất thiết là “tên hiển thị”

Ví dụ:

name = ART-0001
article_name = AI là gì


👉 name = máy dùng
👉 article_name = người dùng nhìn

5️⃣ DOCSTATUS – VÒNG ĐỜI DOCUMENT

Mỗi Document luôn có:

docstatus = 0 | 1 | 2

Giá trị	Ý nghĩa	Sửa được?
0	Draft	✅
1	Submitted	❌
2	Cancelled	❌

👉 DocType thường → chỉ Draft
👉 DocType giao dịch → có Submit

6️⃣ BÀI THỰC HÀNH NHỎ (KHÔNG CODE)
🎯 Mục tiêu

Cảm nhận Document bằng tay

Làm:

Vào Article List

Bấm New

Tạo 2 Article khác nhau

Quay lại List

👉 Quan sát:

Cùng DocType

Nhiều Document

7️⃣ VẬY BƯỚC TIẾP THEO LOGIC LÀ GÌ?

Bạn đã có:

DocType (bản thiết kế)

Document (dữ liệu)

👉 Câu hỏi tiếp theo tự nhiên là:

“Ai được tạo / sửa / xem Document này?”