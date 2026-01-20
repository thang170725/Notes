# open() & .close()
```bash
Để mở file và đóng file.
```
**Syn**
```bash
open(‘data.txt’, ‘w’, encoding=’utf8’)
    + r – Đọc – Giá trị mặc định. Mở tệp để đọc, báo lỗi nếu tệp không tồn tại.
    + a – Thêm – Mở tệp để thêm, tạo tệp nếu tệp không tồn tại. Thêm vào cuối file.
    + w – Ghi – Mở tệp để ghi, tạo tệp nếu tệp không tồn tại. Ghi đè nếu file có nội dung trước đó.
    + t – Văn bản – Giá trị mặc định. Chế độ văn bản.
    + b – Nhị phân – Chế độ nhị phân (Ví dụ: hình ảnh).
    + "w+"  : Đọc + ghi đè	
    + "a+"  : Đọc + ghi tiếp	
    + "r+"  : Đọc + ghi (không xóa)	
```