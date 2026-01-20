# .remove()
```bash
Để xóa một phần tử ra khỏi tuple.
```
**Syn** 
```bash
<variable>.remove(value)
```
**Ex**
```python
myTuple = (1,2,3)
a = list(myTuple)
a.remove(3)
myTuple = tuple(a)
print(myTuple) # (1, 2)
```