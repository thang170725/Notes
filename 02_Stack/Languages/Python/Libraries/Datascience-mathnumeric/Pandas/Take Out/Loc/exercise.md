# Lấy ra một hàng theo index
```python
import pandas as pd

data = {
    "full_name": ["John", "Jane", "Tom", 'Quoc'],
    "address": ["New York", "HaNoi", "Tokyo", 'HCM'],
    'country': ['USA', 'Viet Nam', 'Japan', 'Viet Nam']
    }
df = pd.DataFrame(data)

print(df.loc[1])
print(list(df.loc[1]))

# full_name        Jane
# address         HaNoi
# country      Viet Nam
# Name: 1, dtype: object
# ['Jane', 'HaNoi', 'Viet Nam']
```

# lấy nhiều hàng theo nhiều index
```python
import pandas as pd

data = {
    "full_name": ["John", "Jane", "Tom", 'Quoc'],
    "address": ["New York", "HaNoi", "Tokyo", 'HCM'],
    'country': ['USA', 'Viet Nam', 'Japan', 'Viet Nam']
    }
df = pd.DataFrame(data)

print(df.loc[[1, 2]])
```

# Lấy theo điều kiện
```python
import pandas as pd

data = {
    "full_name": ["John", "Jane", "Tom", 'Quoc'],
    "address": ["New York", "HaNoi", "Tokyo", 'HCM'],
    'country': ['USA', 'Viet Nam', 'Japan', 'Viet Nam']
    }
df = pd.DataFrame(data)

print(df.loc[df['country'] == 'Viet Nam'])
```

# lấy theo điều kiện đồng thời thay đổi theo điều kiện
```python
import pandas as pd

data = {
    "full_name": ["John", "Jane", "Tom", 'Quoc'],
    "address": ["New York", "HaNoi", "Tokyo", 'HCM'],
    'country': ['USA', 'Viet Nam', 'Japan', 'Viet Nam'],
    'salary': [10, 20, 30, 10]
    }
df = pd.DataFrame(data)
df.loc[df['country'] == 'Viet Nam', 'salary'] += 10
print(df)
```