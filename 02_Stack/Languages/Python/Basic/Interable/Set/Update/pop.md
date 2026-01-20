# .pop()
```bash
Bạn cũng có thể sử dụng phương thức pop để xóa một mục, nhưng phương thức này sẽ xóa một mục ngẫu nhiên, do đó bạn không thể chắc chắn mục nào sẽ bị xóa.
```
**Syn** 
```bash
<variable>.pop()
```
**Ex**
```python
mySet= {"apple", "banana", "orange", "Lemon", "Passion"}
x = mySet.pop()

print(x) # orange
print(mySet) # {'apple', 'banana', 'Lemon', 'Passion'}
```