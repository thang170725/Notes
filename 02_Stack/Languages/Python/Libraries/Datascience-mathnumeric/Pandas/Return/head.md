# .head()
```bash
- Một trong những phương pháp được sử dụng nhiều nhất để có được cái nhìn tổng quan nhanh về DataFrame là phương pháp head().
- head() trả về các tiêu đề và số lượng hàng được chỉ định, bắt đầu từ trên cùng hoặc lấy ra n dòng đầu tiên.
```
**Ex**
```python
import pandas as pd

df = pd.read_csv('data.csv')

print(df.head(10)) # lấy ra 10 dòng dầu tiên
print(df.head()) # tự động lấy ra 5 dòng đầu tiên (mặc địch)

#    Duration  Pulse  Maxpulse  Calories
# 0        60    110       130     409.1
# 1        60    117       145     479.0
# 2        60    103       135     340.0
# 3        45    109       175     282.4
# 4        45    117       148     406.0
# 5        60    102       127     300.5
# 6        60    110       136     374.0
# 7        45    104       134     253.3
# 8        30    109       133     195.1
# 9        60     98       124     269.0
#    Duration  Pulse  Maxpulse  Calories
# 0        60    110       130     409.1
# 1        60    117       145     479.0
# 2        60    103       135     340.0
# 3        45    109       175     282.4
# 4        45    117       148     406.0
```