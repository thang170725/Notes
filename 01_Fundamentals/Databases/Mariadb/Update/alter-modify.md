- [Đổi kiểu dữ liệu cho một cột](#đổi-kiểu-dữ-liệu-cho-một-cột)

---

# Đổi kiểu dữ liệu cho một cột
```bash
ALTER TABLE ten_bang
MODIFY COLUMN ten_cot KIEU_DU_LIEU_MOI;
```

# Đổi kiểu dữ liệu và thêm khóa chính
```sql
ALTER TABLE districts
MODIFY COLUMN id INT UNSIGNED NOT NULL AUTO_INCREMENT,
ADD PRIMARY KEY (id);
```