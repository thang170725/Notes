# .rename()
```bash
- Dùng để đổi tên cột hoặc chỉ mục của dataframe.
```
**Ex**
```bash
DataFrame.rename(
    mapper=None,
    *,
    index=None,
    columns=None,
    axis=None,
    copy=None,
    inplace=False,
    level=None,
    errors='ignore'

- errors
    + ignore' (mặc định): không lỗi nếu tên không tồn tại
    + 'raise': báo lỗi nếu không tìm thấy tên cần đổi
)
```
**Ex**
```python
import pandas as pd

data = {
    "user_name": ['thang', 'minh'],
    "user_email": ['leducthang', 'nguyenngocminh']
}

mapping = {
"user_name": "name",
"user_email": "email"
}

df = pd.DataFrame(data)
df = df.rename(columns=mapping)

print(df)

#     name           email
# 0  thang      leducthang
# 1   minh  nguyenngocminh
```