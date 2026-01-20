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