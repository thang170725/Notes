Kết nối & thực thi SQL thuần (CORE)
from sqlalchemy import text

with engine.connect() as conn:
    result = conn.execute(text("SELECT * FROM users"))
    rows = result.fetchall()


👉 text() = bắt buộc khi viết SQL string

5️⃣ Insert / Update / Delete (CORE)
Insert
sql = text("""
INSERT INTO users (user_id, full_name, age)
VALUES (:id, :name, :age)
""")

with engine.begin() as conn:
    conn.execute(sql, {
        "id": 1,
        "name": "An",
        "age": 25
    })


👉 engine.begin() = tự commit / rollback

Batch insert (NHANH)
data = [
    {"id": 1, "name": "An", "age": 25},
    {"id": 2, "name": "Binh", "age": 30}
]

with engine.begin() as conn:
    conn.execute(sql, data)


🔥 Nhanh hơn vòng for rất nhiều

6️⃣ Tích hợp với pandas (thực tế nhất)
Read từ DB
import pandas as pd

df = pd.read_sql("SELECT * FROM users", engine)

Ghi vào DB
df.to_sql(
    "users",
    con=engine,
    if_exists="append",
    index=False
)


👉 Đây là lý do lớn nhất dùng SQLAlchemy

7️⃣ Định nghĩa bảng (Table metadata)
from sqlalchemy import Table, Column, Integer, String, MetaData

metadata = MetaData()

users = Table(
    "users",
    metadata,
    Column("user_id", Integer),
    Column("full_name", String(100)),
    Column("age", Integer)
)

Tạo bảng
metadata.create_all(engine)

8️⃣ Query không viết SQL string (Core Expression)
from sqlalchemy import select

stmt = select(users).where(users.c.age > 25)

with engine.connect() as conn:
    result = conn.execute(stmt)
    print(result.fetchall())