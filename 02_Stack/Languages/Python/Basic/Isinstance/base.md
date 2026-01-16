```bash
Trả về true nếu đối tượng được chỉ định thuộc loại được chỉ định, nếu không thì trả về false.
```
**Ex**
```python
isinstance(object, type)
x = isinstance("Hello", (str, float, int, str, list, dict, tuple))
print(x) # True
```