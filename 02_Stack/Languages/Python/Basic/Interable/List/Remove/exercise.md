# xóa phần tử nhỏ hơn 2 trong list
**Ex1**
```python
a = [1, 2, 3, 4, 2, 1.5]
a = [x for x in a if x >= 2]

print(a)
```
**Ex2: Duyệt ngược index**
```python
a = [1, 2, 3, 4, 2, 1.5]

for i in range(len(a) - 1, -1, -1):
    if a[i] < 2:
        del a[i]

print(a)
```