# read_csv
Dùng để tải dữ liệu từ tệp CSV vào python.
**Syn**
```bash
li = pd.read_csv(
    "danhSach.csv", 
    sep=',',
    index=[], 
    encoding=’utf-8’,
    dtype=str,
    na_values=["", "NULL", "None"]
) # dữ liệu hiển thị dưới dạng dataframe

- sep   : Phân cách
```


