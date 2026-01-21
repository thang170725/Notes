# del (câu lệnh)
```bash
- Xóa phần tử theo chỉ số (index)
- Xóa một đoạn (slice)
- Xóa toàn bộ list (biến list bị xóa)
```
**Syn**
```bash
del list[index]
del list[start:end]
del list
```
**Syn**
```python
a = [1, 2, 3, 4, 5]

del a[2]        # xóa phần tử tại index 2
print(a)        # [1, 2, 4, 5]

del a[1:3]     # xóa các phần tử từ index 1 đến 2
print(a)        # [1, 5]

del a
print(a)   # ❌ NameError (a không còn tồn tại vì đã xóa)
```