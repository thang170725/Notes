# pd.notnull() 
```bash
- Là hàm kiểm tra dữ liệu KHÔNG bị thiếu trong pandas.
- pd.notnull(df) = giá trị có dữ liệu → True, bị thiếu → False
- Pandas coi các giá trị sau là missing:
    + NaN
    + None
    + NaT (thời gian)
    + pd.NA
```
**Syn**
```bash
pd.notnull(obj)

- obj có thể là: scalar, Series, DataFrame
```
**Ex**
```python
iimport pandas as pd
import numpy as np

df = pd.DataFrame({
    'name': ['An', None, 'Chi'],
    'age': [20, np.nan, 25]
})
check = pd.notnull(df)

print(df)
print(check)

   name   age
0    An  20.0
1  None   NaN
2   Chi  25.0
    name    age
0   True   True
1  False  False
2   True   True
```