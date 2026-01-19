DataFrame.to_sql() (CỐT LÕI)
df.to_sql(
    name="table_name",
    con=engine,
    if_exists="append",   # fail | replace | append
    index=False,
    chunksize=1000
)

Giải thích:

append: insert

replace: drop + create lại

chunksize: insert theo batch (rất quan trọng với file lớn)