



## Bài tập
### Thuật toán tìm ước chung lớn nhất
```python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a
```
