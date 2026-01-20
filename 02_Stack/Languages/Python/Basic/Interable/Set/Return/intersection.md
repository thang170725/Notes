# .intersection()
```bash
Trả về một set mới chỉ chứa các phần tử có trong cả 2 set cũ.
```
**Syn** 
```bash
<variable1>.intersection(<variable2>)
```
**Ex**
```python
mySet= {"apple", "banana", "orange", "Lemon"}
orther = {"orange", "Lemon", "Passion"}

Set = mySet.intersection(orther)

print(Set) # {'Lemon', 'orange'}
```

# &
**Ex2**
```python
mySet= {"apple", "banana", "orange", "Lemon"}
orther = {"orange", "Lemon", "Passion"}
Set = mySet & orther

print(Set) # {'Lemon', 'orange'}
```