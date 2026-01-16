# Thêm khóa ngoài
```sql
ALTER TABLE listings
ADD CONSTRAINT fk_districts
FOREIGN KEY (id_districts)
REFERENCES districts(id)
ON UPDATE CASCADE
ON DELETE RESTRICT;
```