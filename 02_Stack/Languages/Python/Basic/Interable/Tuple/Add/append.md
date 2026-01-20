# .append()
```bash
Để thêm một phần tử nào đó vào tuple. Cần phải chuyển sang kiểu dữ liệu list rồi mới thêm.
```
**syn**
```bash
<variable>.append(value)
```
**Ex**
```python
myTuple = (1,2,3)
a = list(myTuple)
a.append(4)
myTuple = tuple(a)
print(myTuple) # (1, 2, 3, 4)
```
**Ex2**
```python
myTuple = (1,2,3)
a = (4,)
myTuple += a
print(myTuple) # (1, 2, 3, 4)
```