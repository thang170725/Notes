- [Kiểu dữ liệu](#kiểu-dữ-liệu)
- [Tạo | Thêm](#tạo--thêm)
  - [create database](#create-database)
  - [Use](#use)
  - [create table \& primary key \& foreign key](#create-table--primary-key--foreign-key)
  - [auto\_increment](#auto_increment)
- [Xem](#xem)
  - [Select](#select)
  - [show table](#show-table)
  - [Describe](#describe)

---

# Kiểu dữ liệu
```bash
CHAR(n)         : Kiểu chuỗi với độ dài cố định
NCHAR(n)        : Kiếu chuỗi với độ dài cố định hỗ trợ UNICODE
VARCHAR(n)      : Kiểu chuỗi với độ dài chính xác
NVARCHAR(n)     : Kiểu chuỗi với độ dài chính xác hỗ trợ UNICODE
TEXT            : Dữ liệu kiếu chuỗi với độ dài lớn (tối đa 2,147,483,647 ký tự)
NTEXT           : Dữ liệu kiếu chuỗi với độ dài lớn và hỗ trợ UNICODE (tối đa 1,073,741,823 ký tự
INT             : kiểu số nguyên
TINYTINT        : Số nguyên có giá trị từ -231 đến 231 - 1
FLOAT           : Số thực có giá trị từ -1.79E+308 đến 1.79E+308
double          : Kiểu số thực.
DECIMAL(p,s)    : Tương tự kiểu Numeric
enum            : kiểu giữ liệu bắt buộc phải có giá trị
MONEY           : Kiểu tiền tệ
DATETIME        : Kiểu ngày giờ (chính xác đến phần trăm của giây)
SMALLDATETIME   : Kiểu ngày giờ (chính xác đến phút)

Như kiểu Integer
Số nguyên có giá trị từ 0 đến 255.
▪ SMALLINT
▪ BIGINTSố nguyên có giá trị từ -215 đến 215 – 1
Số nguyên có giá trị từ -263 đến 263-1 NUMERIC (p,s) Kiểu số

với độ chính xác cố định.

REAL
Số thực có giá trị từ -3.40E + 38 đến 3.40E + 38

▪ BIT
Kiểu bit (có giá trị 0 hoặc 1)

▪ BINARY

Dữ liệu nhị phân với độ dài cố định (tối đa 8000 bytes)
VARBINARY Dữ liệu nhị phân với độ dài chính xác (tối đa 8000 bytes)
IMAGE
```

# Tạo | Thêm
## create database
Dùng để tạo database.
**Syn**
```sql
create database MyDatabase  -- Tạo một database
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci; -- Như vậy mặc định schema MyDatabase sẽ dùng utf8mb4 + utf8mb4_unicode_ci
```

## Use
Dùng để chọn database.
**Syn**
```sql
use MyDatabase;
```

## create table & primary key & foreign key
Tạo bảng, khóa chính và khóa ngoài.
**Syn**
```sql
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
);
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID)
    REFERENCES Persons(PersonID)
);
```

insert into
Dùng để thêm dữ liệu vào bảng.
Cú pháp:
INSERT INTO Students (studentId, userId, fullNameStudent, major, className)
VALUES (1, 101, 'Nguyễn Văn A', 'Công nghệ thông tin', 'CNTT01');
INSERT INTO Students (studentId, userId, fullNameStudent, major, className)
VALUES
(2, 102, 'Trần Thị B', 'Khoa học máy tính', 'KHMT01'),
(3, 103, 'Lê Văn C', 'Hệ thống thông tin', 'HTTT01');

## auto_increment
Để tạo cột tự tăng. bắt buộc kiểu int
**Syn**
```sql
CREATE TABLE Test (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50)
); -- id sẽ tự động tăng 1 mỗi lần bạn INSERT.

-- Bạn chỉ cần thêm dữ liệu như:
-- INSERT INTO Test (name) VALUES ('Thắng');
-- INSERT INTO Test (name) VALUES ('Nam');
```


# Xem
## Select
Dùng để xem dữ liệu trong bảng.
```bash
SELECT * FROM Students;
```
**Ex**
```sql
SELECT
    s.studentId,
    s.fullNameStudent,
    s.major,
    s.className,
    u.email,
    u.role
FROM Students s
JOIN Users u ON s.userId = u.userId;
SELECT
    c.courseName,
    s.fullNameStudent,
    t.fullNameTeacher,
    t.department
FROM Courses c
JOIN Students s ON c.studentId = s.studentId
JOIN Teachers t ON c.teacherId = t.teacherId;
Xem danh sách gắn với một điều kiện nào đó:
SELECT * FROM Courses WHERE courseId = '2';
```

## show table
Dùng để xem tên các bảng trong db.
**Syb**
```bash
show tables;
```

## Describe
Xem kiểu dữ liệu và toàn bộ dữ liệu của bảng.
Cú pháp:
DESCRIBE Schedules;
-- hoặc
DESC Schedules;

Chỉnh sửa
Đổi charset/collation của database
Cú pháp:
ALTER DATABASE MyDatabase
    CHARACTER SET = utf8mb4
    COLLATE = utf8mb4_unicode_ci;
Đổi charset/collation của một bảng
Cú pháp:
ALTER TABLE Students
    CONVERT TO CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci;
ALTER TABLE Students
    MODIFY fullNameStudent VARCHAR(50)
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci;
Đổi kiểu dữ liệu cho một cột
ALTER TABLE ten_bang
MODIFY COLUMN ten_cot KIEU_DU_LIEU_MOI;
Đổi tên cột trong bảng
ALTER TABLE ten_bang CHANGE ten_cot_cu ten_cot_moi kieu_du_lieu;
order by 
Dùng để sắp xếp kết quả của câu query theo một (hoặc nhiều) cột.
Cập nhật giá trị cho một cột trong một hàng hoặc nhiều hàng
UPDATE Students
SET major = 'Trí tuệ nhân tạo'
WHERE studentId = 1;
UPDATE Students
SET
    major = 'Khoa học máy tính',
    className = 'CS02'
WHERE studentId = 1;

Xóa
Xóa bảng
Cú pháp:
DROP TABLE Students;
Xóa một cột trong bảng
Cú pháp:
ALTER TABLE ten_bang
DROP COLUMN ten_cot;
ALTER TABLE Students
DROP COLUMN className,
DROP COLUMN major;
Xóa dữ liệu một hoặc nhiều hàng
Cú pháp:
DELETE FROM Students
WHERE studentId = 's001';
DELETE FROM Students
WHERE className = 'IT01';
DELETE FROM Users
WHERE userId IN ('s001', 's002', 's003');
