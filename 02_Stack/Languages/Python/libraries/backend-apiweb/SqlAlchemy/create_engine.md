# Tạo kết nối (Engine) – CƠ BẢN NHẤT
```python
from sqlalchemy import create_engine

engine = create_engine(
    "mysql+mysqlconnector://user:password@localhost:3306/db_name",
    echo=False
)
```
Cú pháp connection string
dialect+driver://username:password@host:port/database


Ví dụ:

mysql+pymysql://root:123456@127.0.0.1:3306/testdb