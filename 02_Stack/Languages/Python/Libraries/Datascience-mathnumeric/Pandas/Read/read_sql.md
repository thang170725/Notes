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
**Khi nào NÊN dùng read_sql?**
```bash
- NÊN:
    + Làm data analysis
    + Tool admin
    + Export dữ liệu
    + Notebook / script
    + Báo cáo
KHÔNG NÊN:
    + API backend realtime
    + CRUD business logic
    + Query lớn streaming (vì load hết vào RAM)
```
**So sánh read_sql vs SQLAlchemy Core**
```bash
Tiêu chí	    read_sql	Core
Output	        DataFrame	Row / Mapping
Hiệu năng	    Trung bình	Cao
Memory	        Load all	Có thể stream
Dùng cho API	❌	        ✅
Dùng cho report	✅	        ⚠️
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
**Ex1: Dùng SQL STRING (đơn giản nhất)**
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
**Ex2: Bind parameter (RẤT QUAN TRỌNG)**
```python
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

# An toàn
```
**Ex3: Dùng SQLAlchemy Table + select (chuẩn hơn)**
```python
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


# read_sql nhận trực tiếp Select object
# Không cần convert sang string
```
1. Ví dụ 4 – Đặt index cho DataFrame
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