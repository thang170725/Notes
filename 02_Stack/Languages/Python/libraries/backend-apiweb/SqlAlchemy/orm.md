ORM (chỉ khi cần)
Model
from sqlalchemy.orm import declarative_base
from sqlalchemy import Column, Integer, String

Base = declarative_base()

class User(Base):
    __tablename__ = "users"

    user_id = Column(Integer, primary_key=True)
    full_name = Column(String(100))
    age = Column(Integer)

Session
from sqlalchemy.orm import sessionmaker

Session = sessionmaker(bind=engine)
session = Session()

session.add(User(user_id=3, full_name="Cuong", age=28))
session.commit()


👉 Không nên dùng ORM cho import CSV lớn

🔟 Khi nào dùng cái gì?
Trường hợp	Nên dùng
Import CSV	Core + pandas
ETL	Core
Script DB	Core
Web App	ORM
Data lớn	Core
CRUD nhỏ	ORM
1️⃣1️⃣ Lỗi thường gặp
❌ Quên commit

➡️ dùng engine.begin()

❌ Viết SQL string không dùng text()

➡️ lỗi runtime

❌ Insert chậm

➡️ dùng batch list of dict

1️⃣2️⃣ Cheat sheet nhanh
# Kết nối
engine = create_engine(...)

# Execute
conn.execute(text("SQL"))

# Transaction
with engine.begin() as conn: ...

# pandas
df.to_sql(...)
pd.read_sql(...)

# ORM
session.add()
session.commit()