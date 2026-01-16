# .drop()
```bash
- Là một phương thức dùng để xóa hàng (row) hoặc cột (column) khỏi DataFrame.
```
**Syn**
```bash 
DataFrame.drop(labels=None, axis=0, inplace=False)
    + labels: Tên hàng hoặc cột cần xóa.
    + axis: Xác định loại đối tượng cần xóa. 0 hoặc index – xóa theo hàng, 1 hoặc columns – xóa theo cột.
    + inplace: False (mặc định) trả về một bản sao mới của dataframe. True là thay đổi trực tiếp trên DataFrame gốc.
```
**Ex**
```python
import pandas as pd

# dữ liệu gốc dạng chuỗi
df = pd.DataFrame({
    'name': ['Lan', 'Mai', 'Huy'],
    'age': [19, 20, 21]}
)

print("DataFrame ban đầu\n", df)

newDf = df.drop('age', axis=1) # xóa cột age
print(newDf)

newDf1 = df.drop(0, axis=0) # xóa hàng đầu tiên
print(newDf1)

# DataFrame ban đầu
# name  age
# 0  Lan   19
# 1  Mai   20
# 2  Huy   21
#  name
# 0  Lan
# 1  Mai
# 2  Huy
# name  age
# 1  Mai   20
# 2  Huy   21
```