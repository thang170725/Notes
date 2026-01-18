# .argmin()
```bash
Vị trí phần tử nhỏ nhất.
```
**Syn**
```bash
numpy.argmin(a, axis=None)
```
**Ex1: Mảng 1 chiều**
```python
import numpy as np

a = np.array([10, 5, 7, 4, 8])
print(np.argmin(a)) # 3

# Giá trị nhỏ nhất là 3, nằm ở index 3
```
**Ex2: Mảng 2 chiều**
```python
a = np.array([[4, 2, 9],
              [1, 6, 3]])

print(np.argmin(a, axis=0)) # Theo cột
print(np.argmin(a, axis=1)) # Theo hàng

# Kết quả
# [1 0 1]
# [1 2]
```

# .argmax()
```bash
Vị trí phần tử lớn nhất
```
**Syn**
```bash
numpy.argmax(a, axis=None)
```
**Ex1**
```python
a = np.array([[4, 2, 9],
              [1, 6, 3]])

print(np.argmax(a))          # flatten
print(np.argmax(a, axis=0))  # theo cột
print(np.argmax(a, axis=1))  # theo hàng

# Kết quả
# 2
# [0 1 0]
# [2 1]
```