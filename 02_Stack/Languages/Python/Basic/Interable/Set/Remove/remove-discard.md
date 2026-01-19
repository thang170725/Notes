# .remove()
```bash
Để xóa một phần tử ra khỏi set. Nếu không tìm thấy phần tử cần xóa từ ném ra lỗi.
```
**Syn** 
```bash
<variable>.remove(value)
```
**Ex**
```python
mySet= {"apple", "banana"}
mySet.remove("banana")
print(mySet) # {'apple'}
```

# .discard()
```bash
Để xóa một phần tử ra khỏi set. Nếu không tìm thấy phần tử cần xóa thì bỏ qua lệnh này.
```
**Syn**
```bash
<variable>.discard(value)
```
**Ex**
```python
mySet= {"apple", "banana"}
mySet.discard("banana")
print(mySet) # {'apple'}
```