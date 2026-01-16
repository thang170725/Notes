# Demo Insert district
```python
from sqlalchemy import insert

stmt = insert(districts).values(
    name="Ba Đình",
    city="Hà Nội"
)

with engine.begin() as conn:
    result = conn.execute(stmt)
    district_id = result.inserted_primary_key[0]

Tương đương LAST_INSERT_ID()
```

# Demo Insert listing (FK)
```python
stmt = insert(listings).values(
    id_districts=district_id,
    price_total=56000000000,
    area=96,
    property_type="nha_mat_pho"
)

with engine.begin() as conn:
    conn.execute(stmt)
```

# Demo Insert 2 bảng trong 1 transaction (chuẩn)
```bash
with engine.begin() as conn:
    result = conn.execute(
        insert(districts).values(name="Ba Đình", city="Hà Nội")
    )
    district_id = result.inserted_primary_key[0]

    conn.execute(
        insert(listings).values(
            id_districts=district_id,
            price_total=56000000000,
            area=96
        )
    )
```