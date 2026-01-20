# intersection_update()
```bash
Chỉ giữ lại các phần tử trùng lặp, nhưng nó sẽ thay đổi tập hợp gốc thay vì trả về tập hợp mới.
```
**Syn**
```bash 
<variable1>.intersection_update(<variable2>)
```
**Ex**
```python
mySet= {"apple", "banana", "orange", "Lemon"}
orther = {"orange", "Lemon", "Passion"}
mySet.intersection_update(orther)

print(mySet) # {'orange', 'Lemon'}
```