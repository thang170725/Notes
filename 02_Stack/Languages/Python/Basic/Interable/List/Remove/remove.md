# remove() (phương thức của list)
```bash
- Xóa phần tử đầu tiên có giá trị = value.
```
**Syn**
```python
list.remove(value)
```

a = [1, 2, 3, 2, 4]
a.remove(2)
print(a)   # [1, 3, 2, 4]


⚠️ Nếu không có giá trị cần xóa:

a.remove(10)  # ❌ ValueError