# MetaData
```bash
- MetaData là “registry + context” chứa toàn bộ thông tin schema của database trong SQLAlchemy Core.
- Nói dễ hiểu hơn:
    + Table = 1 bảng
    + MetaData = bản đồ các bảng
    + Engine = kết nối DB
    + Connection = phiên làm việc
- MetaData KHÔNG kết nối DB
- MetaData KHÔNG chứa dữ liệu. Nó chỉ ghi nhớ cấu trúc của các bảng.
```
**Nếu KHÔNG có MetaData thì sao?**
```bash
- Không làm được mấy việc sau:
    + Quan hệ giữa các bảng
```
**Syn**
```bash
from sqlalchemy import MetaData

metadata = MetaData()
```

**Ex1: MetaData chứa Table (cách bạn đang dùng)**
```python
from sqlalchemy import MetaData, Table

metadata = MetaData()

users = Table(
    "users",
    metadata,
    autoload_with=engine
)

orders = Table(
    "orders",
    metadata,
    autoload_with=engine
)

Lúc này: metadata.tables
Output (dict-like):
{
  'users': <sqlalchemy.Table users>,
  'orders': <sqlalchemy.Table orders>
}

```
**Ex2: Vì sao dùng chung MetaData là QUAN TRỌNG**
```python
Table("users", MetaData(), autoload_with=engine)
Table("orders", MetaData(), autoload_with=engine)

# Hậu quả:
# Sai cách (mỗi bảng một metadata)
# SQLAlchemy không biết 2 bảng liên quan gì
# Không join được chuẩn
# Không quản lý được schema

metadata = MetaData()

users = Table("users", metadata, autoload_with=engine)
orders = Table("orders", metadata, autoload_with=engine)
```

6. Demo 3: Join 2 bảng nhờ MetaData

Giả sử:

orders.user_id → users.id

from sqlalchemy import select

stmt = (
    select(
        users.c.email,
        orders.c.total_amount
    )
    .select_from(
        users.join(
            orders,
            users.c.id == orders.c.user_id
        )
    )
)


👉 Join KHÔNG cần ORM, chỉ cần:

Table

MetaData dùng chung

7. Demo 4: MetaData + create_all (ít dùng khi DB có sẵn)
metadata = MetaData()

Table(
    "logs",
    metadata,
    Column("id", Integer, primary_key=True),
    Column("message", String(255))
)

metadata.create_all(engine)


👉 SQLAlchemy sẽ:

Đọc metadata.tables

Tạo bảng tương ứng

8. Demo 5: Reflect toàn bộ DB bằng MetaData
metadata = MetaData()
metadata.reflect(bind=engine)

print(metadata.tables.keys())


👉 Output:

dict_keys(['users', 'orders', 'products'])


➡️ MetaData lúc này là “ảnh chụp” toàn bộ DB

9. Liên hệ với TableFactory của bạn

Class bạn viết:

self.metadata = MetaData()


👉 Ý nghĩa:

Tất cả bảng load từ TableFactory

Đều nằm trong 1 registry

Join, reuse, cache đều OK

👉 Đây là cách làm đúng.

10. Khi nào nên có NHIỀU MetaData?

Hiếm, nhưng có:

Multi-database

Multi-tenant

Migrate schema độc lập

Ví dụ:

user_metadata = MetaData()
log_metadata = MetaData()