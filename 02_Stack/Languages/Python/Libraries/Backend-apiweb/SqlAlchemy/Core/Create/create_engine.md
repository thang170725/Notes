```bash
- Kết nối database, Gửi câu SQL, Không biết bảng nào, cột nào.
- Là điểm khởi đầu cho:
    + ORM (Session)
    + Core (engine.connect(), engine.execute())
- Quan trọng: create_engine() KHÔNG kết nối DB ngay, mà chỉ kết nối khi có query đầu tiên.
```
**Syn**
```bash
from sqlalchemy import create_engine

engine = create_engine(
    "dialect+driver://username:password@host:port/database",
    **options
)

- dialect	mysql, postgresql, sqlite, oracle
- driver	pymysql, psycopg2, cx_oracle
- username	root
- password	123456
- host	    localhost
- port	    3306, 5432
- database	test_db
```
**Ex**
```python
engine = create_engine(
    "mysql+pymysql://root:123456@localhost:3306/mydb",
    echo=True,        # In SQL ra console
    pool_size=5,      # Số connection trong pool
    max_overflow=10   # Số connection vượt pool
)
```
**Ex2**
```python
from sqlalchemy import create_engine

def create_engine_dynamic(cfg):
    url = f"{cfg['driver']}://{cfg['user']}:{cfg['password']}@{cfg['host']}:{cfg['port']}/{cfg['database']}"
    print("DB URL:", url) 
    return create_engine(url)

# ======= LOCAL DEBUG ========
if __name__ == '__main__':
    engine = create_engine_dynamic({
        "driver": "mysql+pymysql",
        "user": "ai_user",
        "password": "ai123",
        "host": "localhost",
        "port": 3306,
        "database": "house_price_project"
    })
    with engine.connect() as conn:
        print('DB CONNECT OK')
```