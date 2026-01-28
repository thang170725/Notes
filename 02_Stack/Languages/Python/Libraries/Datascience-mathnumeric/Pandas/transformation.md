- [.values \& to\_numpy()](#values--to_numpy)
- [.nunique()](#nunique)
- [.sort\_values()](#sort_values)
- [.where()](#where)
- [.concat()](#concat)
---
# .values & to_numpy()
```bash
- values    : Đưa một series, cột trong Dataframe về dạng list.
- to_numpy  : Đưa một series, cột trong Dataframe về dạng numpy array.
```
**Ex1: values**
```python
data = {
        'size': [850, 900, 1200, 1500],
        'bedrooms': [2, 3, 3, 4],
        'age': [10, 15, 20, 5],
        'price': [200000, 250000, 300000, 350000]
    }
df = pd.DataFrame(data)
print(df['size'], df['size'].values)

# 0     850
# 1     900
# 2    1200
# 3    1500
# Name: size, dtype: int64 
# [ 850  900 1200 1500]
```
**Ex2: values[]**
```python
dataFrame = pd.read_csv("danhSach.csv")
x = dataFrame.values[:, 0]

print(x) # [180 175 167 182 175 178 170 170 178 182 167 166 169 168 175 172]
```
**Ex3: to_numpy**
```python
import pandas as pd
data = {
        'size': [850, 900, 1200, 1500],
        'bedrooms': [2, 3, 3, 4],
        'age': [10, 15, 20, 5],
        'price': [200000, 250000, 300000, 350000]
    }
df = pd.DataFrame(data)
df = df['size'].to_numpy()

print(df, type(df)) # [ 850  900 1200 1500] <class 'numpy.ndarray'>
```
# .nunique()
```bash
- Để đếm tổng số lượng các giá trị khác nhau trong một cột nào đó.
```
**Ex**
```python
df = pd.DataFrame({
    "Color": ["Red", "Blue", "Red", "Green", "Blue", "Yellow", "Red"]
})

print(df["Color"].nunique()) # 4
```
# .sort_values()
```bash
- Là hàm sắp xếp của pandas.
```
**Syn**
```bash
df.sort_values(
    by=...,          # cột (hoặc danh sách cột) để sắp xếp
    ascending=True,  # True: tăng dần | False: giảm dần
    inplace=False    # False: trả về DataFrame mới
)
```
**Ex1: Sắp giảm**
```python
import pandas as pd

df = pd.DataFrame({
    'name': ['A', 'B', 'C', 'D'],
    'sum_salary': [12_000_000, 20_000_000, 15_000_000, 20_000_000]
})
df_sorted = df.sort_values(by='sum_salary', ascending=False)

print(df_sorted)

#   name  sum_salary
# 1    B    20000000
# 3    D    20000000
# 2    C    15000000
# 0    A    12000000
```
**Ex2: Sắp xếp theo nhiều cột**
```python
df.sort_values(
    by=['sum_salary', 'name'],
    ascending=[False, True]
)

# Sắp theo sum_salary giảm dần
# Nếu trùng lương → sắp theo name tăng dần
```
# .where()
```bash
- Trong pandas, hàm where() dùng để giữ giá trị khi điều kiện đúng, còn khi sai thì thay bằng giá trị khác (thường là NaN).
- where = “nếu đúng thì giữ, nếu sai thì thay”
```
**Syn**
```bash
DataFrame.where(
    cond,
    other=nan,
    inplace=False,
    axis=None,
    level=None,
    errors='raise',
    try_cast=False
)

- cond      : (bắt buộc). Kiểu: bool, DataFrame/Series boolean, hoặc hàm
- other     : Giá trị thay thế khi điều kiện sai. Mặc định: NaN
- inplace   : False (mặc định): trả về DataFrame mới. True: sửa trực tiếp DataFrame
- axis      : Xác định áp dụng điều kiện theo hàng hay cột. Thường không cần dùng
- level     : Dùng cho MultiIndex. Ít gặp
- error
    + 'raise': báo lỗi nếu cond không khớp shape
    + 'ignore': bỏ qua lỗi
- try_cast  : Cố gắng giữ kiểu dữ liệu cũ. Hiếm khi dùng
```
**Ex**
**Topic**
```bash
Giữ lại lương ≥ 10 triệu, còn lại thay bằng 0
```
**Answer**
```python
import pandas as pd

df = pd.DataFrame({
    'name': ['An', 'Bình', 'Chi'],
    'salary': [8_000_000, 12_000_000, 15_000_000]
})

print(df)

#    name   salary
# 0   An   8000000
# 1  Bình 12000000
# 2  Chi  15000000

df_new = df.where(df['salary'] >= 10_000_000, other=0)

print(df_new)

#    name   salary
# 0   0        0
# 1  Bình 12000000
# 2  Chi  15000000
```
# .concat()
```python
def add_worker(df):
    wid = input("Mã: ")
    name = input("Họ tên: ")
    salary = float(input("Lương/ngày: "))
    days = int(input("Số ngày làm: "))
    allowance = float(input("Phụ cấp: "))

    new_row = {
        "worker_id": wid,
        "name": name,
        "salary": salary,
        "days_work": days,
        "allowance": allowance,
        "sum_salary": salary * days + allowance
    }

    return pd.concat([df, pd.DataFrame([new_row])], ignore_index=True)
```