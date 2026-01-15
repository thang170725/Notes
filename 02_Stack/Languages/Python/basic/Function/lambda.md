```bash
Là một hàm ẩn danh nhỏ. Hàm lambda có thể lấy bất kỳ số lượng đối số nào, nhưng chỉ có thể có, một biểu thức.
```
**Cú pháp** 
```bash
lambda arguments : expression
```
**Ex**
```python
def myfunc(n):
  return lambda a : a * n
mydoubler = myfunc(2)
mytripler = myfunc(3)
print(mydoubler(11)) # 22
print(mytripler(11)) # 33
```