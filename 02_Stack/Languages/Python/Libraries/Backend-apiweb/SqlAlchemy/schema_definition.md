- [Column \& Data-type \& declarative\_base](#column--data-type--declarative_base)
  - [So sánh giữa có và không có declarative\_base](#so-sánh-giữa-có-và-không-có-declarative_base)
- [columns](#columns)
---
# Column & Data-type & declarative_base
```bash
- Column    : Định nghĩa cột trong bảng
```
**Syn: Column**
```bash
Column(
    name,
    type_,
    primary_key=False,
    nullable=True,
    unique=False,
    default=None,
    index=False,
    foreign_key=...
)
```
**Data-type**
```bash
1. String
2. Integer
3. String
```
**declarative_base**
## So sánh giữa có và không có declarative_base
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
# columns
**Ex**
```python
from sqlalchemy import Table, MetaData

def load_table(engine, table_name: str):
    metadata = MetaData()
    return Table(table_name, metadata, autoload_with=engine)

if __name__ == '__main__':
    from backend.python_service.app.core.db import create_engine_dynamic
    engine = create_engine_dynamic({
        "driver": "mysql+pymysql",
        "user": "ai_user",
        "password": "ai123",
        "host": "localhost",
        "port": 3306,
        "database": "house_price_project"
    })
    
    table = load_table(engine, table_name='listings')
    print(table.columns)

# ReadOnlyColumnCollection(listings.id, listings.id_districts, listings.price_total, listings.price_m2, listings.area, listings.location_lat, listings.location_long, listings.dist_to_center, listings.property_type, listings.legal_status, listings.bedrooms, listings.bathrooms, listings.floors, listings.orientation, listings.frontage_width, listings.alley_width, listings.source_url, listings.posted_date, listings.scraped_date, listings.market_trend_idx)
```