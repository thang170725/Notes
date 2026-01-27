- [DataFrame \& Series](#dataframe--series)
---
# DataFrame & Series
```bash
- series    : Cấu trúc dữ liệu 1 chiều.
- DataFrame : Cấu trúc dữ liêụ 2 chiều (dạng bảng).
```
**Syn: DataFrame**
```bash
df = pd.DataFrame(data, index=None, columns=None, dtype=None, copy=False)
- data (dict, list, numpy array, …): Dữ liệu gốc tạo nên bảng.
- index (list hoặc array): Nhãn cho các dòng, mặc địn là 0,1,2, …
- columns (list hoặc array): Tên cho các cột (nếu không sẽ tự động lấy từ data).
- dtype: Ép kiểu dữ liệu cho toàn bộ bảng.
- copy (bool): Nếu True tạo bản sao của dữ liệu gốc.
```
**Ex1: DataFrame**
```python
data = {
        "fullName": ["John", "Duo", "Chicago"],
        "address": ["New York", "Hanoi", "Tokyo"]
}
li = pd.DataFrame(data)
print(li)

#    fullName   address
# 0     John  New York
# 1      Duo     Hanoi
# 2  Chicago     Tokyo
```
**Ex2: Series**
```python
s = pd.Series([0,1,2,3], index=["a","b","c","d"])

# a    0
# b    1
# c    2
# d    3
# dtype: int64
```
# .shape
```bash
- Trả về số lượng hàng cột có trong dataFrame
```
**Ex**
print(df.shape)