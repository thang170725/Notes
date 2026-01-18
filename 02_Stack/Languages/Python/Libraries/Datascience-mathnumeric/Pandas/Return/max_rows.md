# pd.options.display.max_rows
```bash
- Để kiểm tra số hàng tối đa của hệ thống.
```
**Ex**
```python
import pandas as pd

def main():
    pd.options.display.max_rows = 2
    data = {
        "fullName": ["John", "Jane", "Tom"],
        "address": ["New York", "HaNoi", "Tokyo"]
    }
    df = pd.DataFrame(data)
    print(pd.options.display.max_rows)
    print(df)
main()

# 2
#    fullName   address
# 0      John  New York
# ..      ...       ...
# 2       Tom     Tokyo

# [3 rows x 2 columns]
```