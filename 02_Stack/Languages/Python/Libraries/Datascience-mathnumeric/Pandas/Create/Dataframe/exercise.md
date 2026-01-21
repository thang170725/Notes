- [Tạo thêm cột mới trong dataframe](#tạo-thêm-cột-mới-trong-dataframe)
- [Tạo tên cột cho dataframe](#tạo-tên-cột-cho-dataframe)
- [lọc có điều kiện trong dataframe](#lọc-có-điều-kiện-trong-dataframe)

---

# Tạo thêm cột mới trong dataframe
```python
import pandas as pd

data = {
    "full_name": ["John", "Duo", "Chicago"],
    "address": ["New York", "Hanoi", "Tokyo"]
}

df = pd.DataFrame(data)
df['sum'] = df['full_name'] + ' ' + df['address']

print(df)

#   full_name   address            sum
# 0      John  New York  John New York
# 1       Duo     Hanoi      Duo Hanoi
# 2   Chicago     Tokyo  Chicago Tokyo
```

# Tạo tên cột cho dataframe
```python
import pandas as pd

data = [[1,2,3,4,5]] # 1 dòng, 5 cột

df = pd.DataFrame(
    data,
    columns=['1','2','3','4','5']
)
print(df)

#    1  2  3  4  5
# 0  1  2  3  4  5
```

# lọc có điều kiện trong dataframe
```python
import pandas as pd
data = {
    'name': ['thang', 'tien', 'thuy', 'thanh', 'hong'],
    'salary': [10, 20, 8, 5, 9]
}

df = pd.DataFrame(data)
new_df = df[df['salary'] > 8.5]

print(new_df)

#     name  salary
# 0  thang      10
# 1   tien      20
# 4   hong       9
```