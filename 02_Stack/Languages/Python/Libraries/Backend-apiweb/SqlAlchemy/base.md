- [Kiến trúc SQLAlchemy (rất quan trọng)](#kiến-trúc-sqlalchemy-rất-quan-trọng)
- [Kết nối](#kết-nối)
- [Khai báo metadata \& table (map DB thật)](#khai-báo-metadata--table-map-db-thật)

---

```bash
- SQLAlchemy có 2 lớp:
    + Core → gần SQL, dễ hiểu cho người đã biết SQL (👉 khuyên dùng trước)
    + ORM → làm việc với object Python (sẽ dùng sau)
- Cần pip install sqlalchemy pymysql (pymysql = driver cho MariaDB/MySQL)
```

# Kiến trúc SQLAlchemy (rất quan trọng)
SQLAlchemy có 2 tầng:
```bash
Python
 ├── SQLAlchemy ORM   (cao, nhiều magic)
 └── SQLAlchemy Core  (thấp, gần SQL)
       └── DB Driver (mysql-connector / pymysql)
            └── MySQL

- 90% import CSV, ETL → dùng Core
- Web app → ORM
```

# Kết nối
**Syn**
```python
from sqlalchemy import create_engine

engine = create_engine(
    "mysql+pymysql://user:password@localhost:3306/realestate", # mysql+pymysql://root:123456@127.0.0.1:3306/testdb
    echo=False,        # True để debug SQL
    pool_recycle=3600
)
```

# Khai báo metadata & table (map DB thật)
```python
from sqlalchemy import (
    MetaData, Table, Column,
    Integer, String, DECIMAL, Float, Date, DateTime, ForeignKey
)

metadata = MetaData()

districts = Table(
    "districts",
    metadata,
    Column("id", Integer, primary_key=True),
    Column("name", String(50), nullable=False),
    Column("city", String(50), nullable=False),
)

listings = Table(
    "listings",
    metadata,
    Column("id", Integer, primary_key=True),
    Column("id_districts", Integer, ForeignKey("districts.id")),
    Column("price_total", DECIMAL(15, 0)),
    Column("area", DECIMAL(7, 2)),
    Column("property_type", String(30)),
)

# Không gọi metadata.create_all() nếu DB đã tồn tại.
```