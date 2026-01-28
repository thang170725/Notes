- [ls](#ls)
  - [mkdir](#mkdir)
  - [touch](#touch)
---
# ls
```bash
- ls -r: Hiển thị tất cả các file trong các thư mục con.
- ls -a: Hiển thị các file ẩn.
- ls -al: sẽ liệt kê các file và thư mục với thông tin chi tiết như quyền, kích thước, chủ sở hữu, …
4. ls | wc -l       : Đếm TẤT CẢ (file + folder) trong thư mục cha (Ex: ls /home/user/test | wc -l)
5. ls -A | wc -l    : Đếm tất cả kể cả file ẩn
```
File + folder
find . | wc -l

Chỉ file
find . -type f | wc -l

Chỉ folder
find . -type d | wc -l
## mkdir
Tạo ra thư mục
**Syn**
```bash
mkdir git_test
```
## touch
```bash
touch index.html (Tao một file tên là index.html)
```