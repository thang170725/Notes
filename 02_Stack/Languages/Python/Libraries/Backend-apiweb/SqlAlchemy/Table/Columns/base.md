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