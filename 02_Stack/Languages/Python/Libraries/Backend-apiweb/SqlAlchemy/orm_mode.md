- [declarative\_base \& Column \& Data-type](#declarative_base--column--data-type)
- [sessionmaker()](#sessionmaker)
- [.add() \& .commit() \& refresh()](#add--commit--refresh)
---
# declarative_base & Column & Data-type
**Không có declarative_base**
```python
class User:
    __tablename__ = "users"

# SQLAlchemy sẽ coi đây là class Python bình thường
```
**Có declarative_base**
```bash
backend/
├── base.py
├── user.py
```
**base.py**
```python
from sqlalchemy.orm import declarative_base

Base = declarative_base()
```
**user.py**
```python
from sqlalchemy import Column, Integer, String
from backend.db.base import Base

class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True)
    username = Column(String(50))
    password = Column(String(255))

# User class  <=>  users table
```
# sessionmaker()
**Syn**
```bash
from sqlalchemy.orm import sessionmaker

SessionLocal = sessionmaker(
    bind=engine,
    autocommit=False,
    autoflush=False,
)

- bind=engine	    : gắn session với DB
- autocommit=False	: không tự commit
- autoflush=False	: không tự đẩy dữ liệu
- SessionLocal()	: tạo 1 session mới
```
**Ex**
```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "mysql+pymysql://user:pass@localhost/dbname"

engine = create_engine(DATABASE_URL)

SessionLocal = sessionmaker(
    bind=engine,
    autocommit=False,
    autoflush=False,
)
```

# .add() & .commit() & refresh()
```bash
- add       : đưa object vào session chưa ghi xuống db.
- commit    : thực sự insert vào db. nếu lỗi -> rollback
- refresh   : lấy dữ liệu mới nhất từ db
```
**Ex**
```python
@router.post("/register")
def register(
    payload: UserSchema,
    db: Session = Depends(get_db)
):
    user = User(
        **payload.model_dump(exclude_unset=True)
    )

    db.add(user)
    db.commit()
    db.refresh(user)

    return {
        "id": user.id,
        "username": user.username
    }
```