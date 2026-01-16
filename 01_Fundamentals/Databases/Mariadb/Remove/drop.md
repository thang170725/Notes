- [Xóa bảng](#xóa-bảng)
- [Xóa một cột trong bảng](#xóa-một-cột-trong-bảng)
- [Xóa khóa ngoài](#xóa-khóa-ngoài)
- [Xóa khóa chính](#xóa-khóa-chính)
- [Xóa dữ liệu một hoặc nhiều hàng](#xóa-dữ-liệu-một-hoặc-nhiều-hàng)

---

# Xóa bảng
**Syn**
```bash
DROP TABLE Students;
```

# Xóa một cột trong bảng
**Syn**
```bash
ALTER TABLE ten_bang
DROP COLUMN ten_cot;
```
**Ex**
```sql
ALTER TABLE Students
DROP COLUMN className,
DROP COLUMN major;
```

# Xóa khóa ngoài
**Ex**
```sql
alter table listings 
drop foreign key fk_districts;
```

# Xóa khóa chính
```sql
ALTER TABLE districts
DROP PRIMARY KEY;
```

# Xóa dữ liệu một hoặc nhiều hàng
**Ex**
```sql
DELETE FROM Students
WHERE studentId = 's001';
DELETE FROM Students
WHERE className = 'IT01';
DELETE FROM Users
WHERE userId IN ('s001', 's002', 's003');
```