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
**Ex:**
```python

import pandas as pd

df = pd.DataFrame({
    'name': ['A', 'B', 'C', 'D'],
    'sum_salary': [12_000_000, 20_000_000, 15_000_000, 20_000_000]
})

print("=== Dữ liệu ban đầu ===")
print(df)

df_sorted = df.sort_values(by='sum_salary', ascending=False)

print("\n=== Sắp xếp theo tổng lương giảm dần ===")
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