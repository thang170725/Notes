# del
```bash
Để xóa toàn bộ set. Del sẽ xóa cả giá trị set và biến set.
```
**Syn** 
```bash
del <variable>
```
**Ex**
```python
mySet= {"apple", "banana", "orange", "Lemon", "Passion"}
del mySet

print(mySet)

# File "D:\workspace\Python_box\TestPy.py", line 3, in <module>
#    print(mySet)
#     ^^^^^
# NameError: name 'mySet' is not defined
```