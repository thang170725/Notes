# name & type
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
    for col in table.columns:
        print(col.name, col.type)

# id INTEGER
# id_districts INTEGER
# price_total DECIMAL(15, 0)
# price_m2 DECIMAL(15, 2)
# area DECIMAL(7, 2)
# location_lat FLOAT
# location_long FLOAT
# dist_to_center FLOAT
# property_type VARCHAR(30)
# legal_status VARCHAR(50)
# bedrooms TINYINT
# bathrooms TINYINT
# floors TINYINT
# orientation VARCHAR(20)
# frontage_width FLOAT
# alley_width FLOAT
# source_url VARCHAR(500)
# posted_date DATE
# scraped_date DATETIME
# market_trend_idx FLOAT
```