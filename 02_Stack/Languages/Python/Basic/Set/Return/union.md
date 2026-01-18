# .union()
```bash
Trả về một set mới với các giá trị phần tử là 2 set cũ.
```
**Syn**
```bash
<variable>.union(<variable1>, <variable2>, …)
<variable1> | <variable2> | …
```
**Ex1**
```python
mySet= {"apple", "banana", }
orther = {"orange", "Lemon", "Passion"}
Set = mySet.union(orther)
print(Set) # {'banana', 'apple', 'orange', 'Passion', 'Lemon'}
```
**Ex2**
```python
mySet= {"apple", "banana", }
orther = {"orange", "Lemon", "Passion"}
Set = mySet | orther
print(Set) # {'Passion', 'orange', 'Lemon', 'banana', 'apple'}
```