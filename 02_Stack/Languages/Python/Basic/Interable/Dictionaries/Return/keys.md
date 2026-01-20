# .keys()
```bash
- Để lấy ra tên các key.
```
**Syn**
```bash
<variable>.keys()
```
**Ex1**
```python
n = { 1: "một", 2: "hai"}

for i in n.keys():
    print(i)

# 1
# 2
```
**Ex2**
```python
dir = dict(name='John', age=25, city='New York')

print(dir.keys(), type(dir.keys())) # dict_keys(['name', 'age', 'city']) <class 'dict_keys'>
```