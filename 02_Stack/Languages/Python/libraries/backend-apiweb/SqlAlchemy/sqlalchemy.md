```bash
- pip install sqlalchemy
- Dùng MySQL thì cần thêm driver. Khuyên dùng: pip install mysql-connector-python
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