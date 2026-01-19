# pd.read_sql()
```bash
- pandas.read_sql dùng để chạy SQL và trả kết quả về DataFrame.
- Nó là cầu nối giữa:
    + SQL (MariaDB / MySQL / PostgreSQL…)
    + Pandas (DataFrame)
- Rất hay dùng cho:
    + Data analysis
    + Report
    + ETL
    + Export CSV / Excel
    + Test nhanh DB
- read_sql:
    + Mở connection
    + Execute
    + Fetch all
    + Build DataFrame
```
**Syn**
```bash
pandas.read_sql(
    sql,
    con,
    params=None,
    index_col=None,
    parse_dates=None
)

- sql	        : Câu SQL string hoặc SQLAlchemy Select
- con	        : DB connection / engine
- params	    : Bind parameter
- index_col	    : Cột làm index
- parse_dates	: Parse cột ngày
```
**Ex: Dùng SQL STRING (đơn giản nhất)**
```python
import pandas as pd

query = """
SELECT id, name, city
FROM districts
LIMIT 10
"""

df = pd.read_sql(query, con=engine)

print(df)

#    id        name      city
# 0   1     District A   Hanoi
# 1   2     District B   Hanoi
...

```


1. Ví dụ 2 – Bind parameter (RẤT QUAN TRỌNG)
query = """
SELECT id, name
FROM districts
WHERE city = %(city)s
LIMIT %(limit)s
"""

df = pd.read_sql(
    query,
    con=engine,
    params={
        "city": "Hanoi",
        "limit": 5
    }
)


✅ An toàn
❌ Không inject được

5. Ví dụ 3 – Dùng SQLAlchemy Table + select (chuẩn hơn)
from sqlalchemy import select
import pandas as pd

districts = table_factory.get("districts")

stmt = (
    select(
        districts.c.id,
        districts.c.name,
        districts.c.city
    )
    .limit(10)
)

df = pd.read_sql(stmt, con=engine)

print(df.head())


👉 read_sql nhận trực tiếp Select object
👉 Không cần convert sang string

6. Ví dụ 4 – Đặt index cho DataFrame
df = pd.read_sql(
    "SELECT id, name FROM districts",
    con=engine,
    index_col="id"
)


Kết quả:

id trở thành index

7. Ví dụ 5 – Parse datetime
df = pd.read_sql(
    "SELECT id, created_at FROM districts",
    con=engine,
    parse_dates=["created_at"]
)


👉 created_at thành datetime64[ns]

8. Khi nào NÊN dùng read_sql?

✅ NÊN:

Làm data analysis

Tool admin

Export dữ liệu

Notebook / script

Báo cáo

❌ KHÔNG NÊN:

API backend realtime

CRUD business logic

Query lớn streaming (vì load hết vào RAM)

9. So sánh read_sql vs SQLAlchemy Core
Tiêu chí	read_sql	Core
Output	DataFrame	Row / Mapping
Hiệu năng	Trung bình	Cao
Memory	Load all	Có thể stream
Dùng cho API	❌	✅
Dùng cho report	✅	⚠️
10. Liên hệ với kiến trúc bạn đang xây

Bạn đang có:

DatabaseConnection → engine

TableFactory → schema

QueryBuilder → SQL

👉 read_sql nằm trên cùng, dùng khi:

Muốn lấy nhanh data

Không cần repository

Không cần mapping phức tạp

Ví dụ rất hợp với bạn:

sql = MariaDBQueryBuilder.fetch_table_rows(
    table_name="districts",
    fields=["id", "name", "city"],
    limit=10
)

df = pd.read_sql(sql, con=engine)

11. Một câu chốt để nhớ

read_sql = SQL → DataFrame, không phải ORM, không phải repository

Nếu bạn muốn, bước tiếp theo mình có thể:

Demo read_sql với JOIN

So sánh read_sql vs to_sql

Dùng chunksize để xử lý dữ liệu lớn

Gắn read_sql vào pipeline ETL

👉 Bạn định dùng read_sql cho report hay training model?