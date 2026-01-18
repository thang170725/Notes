# loc[]
```bash
- Trả về một hoặc nhiều hàng được chỉ định.
```
**Ex**
```python
import pandas as pd

def main():
    data = {
        "fullName": pd.Series(["John", "Jane", "Tom"]),
        "address": pd.Series(["New York", "HaNoi", "Tokyo"])
    }
    li = pd.DataFrame(data)
    print(li.loc[1])
    print(li)
main()

# fullName     Jane
# address     HaNoi
# Name: 1, dtype: object
#   fullName   address
# 0     John  New York
# 1     Jane     HaNoi
# 2      Tom     Tokyo
```
**Ex2**
```python
import pandas as pd
def main():
    data = {
        "fullName": pd.Series(["John", "Jane", "Tom"]),
        "address": pd.Series(["New York", "HaNoi", "Tokyo"])
    }
    li = pd.DataFrame(data)
    print(li.loc[[1,2]])
    print(li)
main()

#   fullName address
# 1     Jane   HaNoi
# 2      Tom   Tokyo
#   fullName   address
# 0     John  New York
# 1     Jane     HaNoi
# 2      Tom     Tokyo
```