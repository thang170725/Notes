# .values
```bash
Đưa một series, cột trong Dataframe về dạng list.
```
**Ex**
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
# .to_numpy()
```bash
Đưa một series, cột trong Dataframe về dạng numpy array.
```
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
print(df, type(df))

# [ 850  900 1200 1500] <class 'numpy.ndarray'>
```