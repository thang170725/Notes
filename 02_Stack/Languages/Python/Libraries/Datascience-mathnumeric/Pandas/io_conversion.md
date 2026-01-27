- [.read\_csv() \& .to\_csv()](#read_csv--to_csv)
---
# .read_csv() & .to_csv()
```bash
- read_csv  : Đọc từ file csv.
- to_csv    : Ghi dữ liệu vào file csv.
```
**Syn: read_csv**
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