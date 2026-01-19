# Table
```bash
- Table là biểu diễn Python cho một bảng SQL cụ thể trong db.
- Nó KHÔNG:
    + Tạo bảng (trừ khi bạn create_all)
    + Không chạy query
    + Không chứa dữ liệu
- Nó CHỈ:
    + Mô tả schema của bảng
    + Là nguyên liệu để build SQL thuần
- Dùng khi:
    + Viết query thuần
    + Không cần ORM Model
    + DB có sẵn
    + Viết tool, admin, ETL, report
- Không nên dùng Table khi:
    + Domain logic phức tạp
    + Cần relationship
    + App CRUD lớn (lúc đó dùng ORM)
```
**Syn**
```bash
Table(
    table_name,
    metadata,
    Column(...),
    Column(...),
)

Table(
    table_name,
    metadata,
    autoload_with=engine
)

- SQLAlchemy sẽ:
    + Connect DB
    + Read schema
    + Tự tạo Column objects
-> Đây gọi là: Table reflection
```