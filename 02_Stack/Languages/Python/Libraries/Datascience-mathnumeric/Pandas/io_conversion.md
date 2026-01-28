- [.read\_csv() \& .to\_csv()](#read_csv--to_csv)
- [pd.read\_sql()](#pdread_sql)
- [.head()](#head)
- [DataFrame.to\_sql() (CỐT LÕI)](#dataframeto_sql-cốt-lõi)
---
# .read_csv() & .to_csv()
```bash
- read_csv  : Đọc từ file csv.
- to_csv    : Ghi dữ liệu vào file csv.
```
**Syn: read_csv**
```bash
li = pd.read_csv(
    "danhSach.csv", 
    sep=',',
    index=[], 
    encoding=’utf-8’,
    dtype=str,
    na_values=["", "NULL", "None"]
) # dữ liệu hiển thị dưới dạng dataframe

- sep   : Phân cách
```
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
# .head()
```bash
- Một trong những phương pháp được sử dụng nhiều nhất để có được cái nhìn tổng quan nhanh về DataFrame là phương pháp head().
- head() trả về các tiêu đề và số lượng hàng được chỉ định, bắt đầu từ trên cùng hoặc lấy ra n dòng đầu tiên.
```
**Ex**
```python
import pandas as pd

df = pd.read_csv('data.csv')

print(df.head(10)) # lấy ra 10 dòng dầu tiên
print(df.head()) # tự động lấy ra 5 dòng đầu tiên (mặc địch)

#    Duration  Pulse  Maxpulse  Calories
# 0        60    110       130     409.1
# 1        60    117       145     479.0
# 2        60    103       135     340.0
# 3        45    109       175     282.4
# 4        45    117       148     406.0
# 5        60    102       127     300.5
# 6        60    110       136     374.0
# 7        45    104       134     253.3
# 8        30    109       133     195.1
# 9        60     98       124     269.0
#    Duration  Pulse  Maxpulse  Calories
# 0        60    110       130     409.1
# 1        60    117       145     479.0
# 2        60    103       135     340.0
# 3        45    109       175     282.4
# 4        45    117       148     406.0
```
# DataFrame.to_sql() (CỐT LÕI)
```bash
- to_sql dùng để:
    + Tạo bảng mới trong database từ DataFrame
    + Hoặc ghi thêm / ghi đè dữ liệu vào bảng đã có
    + Tự động ánh xạ kiểu dữ liệu Pandas → SQL
    + Thường dùng trong:
ETL (Extract – Transform – Load)
    + Data analysis
    + Machine learning pipeline
    + Báo cáo, dashboard
```
**Syn**
```bash
DataFrame.to_sql(
    name,
    con,
    if_exists='fail',
    index=True,
    index_label=None
)

- name	    : Tên bảng SQL
- con	    : Kết nối database (SQLAlchemy engine hoặc connection)
- if_exists	: Cách xử lý nếu bảng đã tồn tại. if_exists có 3 giá trị:
    + 'fail' → báo lỗi (mặc định)
    + 'replace' → xóa bảng cũ, tạo lại
    + 'append' → ghi thêm dữ liệu
- index 	: Có ghi index của DataFrame vào DB không
```
**Ex**
```python
Ví dụ dễ hiểu (SQLite – đơn giản nhất)
Bước 1: Tạo DataFrame
import pandas as pd

df = pd.DataFrame({
    "id": [1, 2, 3],
    "name": ["An", "Bình", "Chi"],
    "age": [20, 21, 22]
})

DataFrame nhìn như sau:
idnameage1An202Bình213Chi22

Bước 2: Kết nối database (SQLite)
from sqlalchemy import create_engine

engine = create_engine("sqlite:///students.db")

📌 File students.db sẽ được tạo nếu chưa tồn tại.

Bước 3: Ghi DataFrame vào SQL bằng to_sql
df.to_sql(
    name="students",
    con=engine,
    if_exists="replace",
    index=False
)


4. Kết quả giả định trong database
Bảng students được tạo
SELECT * FROM students;

Kết quả:
idnameage1An202Bình213Chi22

Kiểu bảng SQL (giả định)
CREATE TABLE students (
    id INTEGER,
    name TEXT,
    age INTEGER
);


5. Ví dụ ghi thêm dữ liệu (append)
df_new = pd.DataFrame({
    "id": [4],
    "name": ["Dũng"],
    "age": [23]
})

df_new.to_sql(
    name="students",
    con=engine,
    if_exists="append",
    index=False
)

Kết quả sau khi append
idnameage1An202Bình213Chi224Dũng23

6. Lỗi thường gặp ⚠️
❌ Sai tên cột khi append
→ Cột DataFrame phải khớp với cột bảng SQL
❌ Ghi index không mong muốn
index=True

→ tạo thêm cột index trong DB
➡️ thường nên dùng index=False

7. Tóm tắt nhanh
✔ to_sql = ghi DataFrame → SQL table
✔ Hay dùng trong data pipeline
✔ Quan trọng nhất:


name


con


if_exists


index



Nếu bạn muốn:


Ví dụ với MySQL / PostgreSQL


So sánh to_sql vs execute INSERT


Cách đọc ngược lại bằng read_sql


👉 cứ nói, mình làm tiếp cho bạn 👍
```