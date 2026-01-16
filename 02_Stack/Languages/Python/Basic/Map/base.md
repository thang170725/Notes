# map
**Ex**
```python
def Change(n):
    n = int(n)
    return "Số chẵn" if n % 2 == 0 else "Số lẻ"

n = input("Nhập các số cách nhau bởi dấu cách: ").split()
res = list(map(Change, n))
print(res)
```