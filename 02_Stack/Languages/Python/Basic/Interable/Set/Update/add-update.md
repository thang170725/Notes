# .add()
```bash
Để thêm một phần tử vào trong một set. 
```
**Syn**
```bash
<variable>.add(value)
```
**Ex**
```python
thisset = {"apple", "banana", "cherry"}
thisset.add("orange")
print(thisset) # {'apple', 'cherry', 'banana', 'orange'}
```

# .update()
```bash
Để thêm các mục từ tập hợp khác vào tập hợp hiện tại.
```
**Syn**  
```bash
<variable>.update(value)
```
**Ex**
```python
mySet= {"apple"}
orther = {"banana"}
mySet.update(orther)
print(mySet) # {'apple', 'banana'}
```