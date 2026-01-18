# .sum()
```bash
Để tính tổng. Trả về một số thực hoặc nguyên
```
**Syn**
```bash
numpy.sum(a, axis=None, dtype=None, out=None, keepdims=False, initial=0, where=True)

- a         : Mảng đầu vào (array-like)
- axis:	    : Trục cần tính tổng (None, 0, 1, tuple…)
- dtype:	: Kiểu dữ liệu của kết quả
- out	    : Mảng để lưu kết quả
- keepdims	: Giữ nguyên số chiều sau khi sum
- initial	: Giá trị khởi tạo cho phép cộng
-where	    : Điều kiện để chọn phần tử khi tính tổng
```
**Ex1: Sum toàn bộ mảng**
```python
import numpy as np

a = np.array([1, 2, 3, 4])
print(np.sum(a)) # 10
```
**Ex2: Sum theo trục (axis)**
```python
a = np.array([[1, 2, 3],
              [4, 5, 6]])

print(np.sum(a, axis=0)) # Sum theo cột
print(np.sum(a, axis=1)) # Sum theo hàng

# Kết quả
# [5 7 9]
# [ 6 15]
```
**Ex3: Giữ nguyên số chiều (keepdims=True)**
```python
print(np.sum(a, axis=1, keepdims=True))

# Kết quả
# [[ 6]
#  [15]]
# Hữu ích khi muốn broadcast với mảng ban đầu.
```
**Ex4: Chỉ định kiểu dữ liệu (dtype)**
```python
a = np.array([1, 2, 3], dtype=np.int8)
print(np.sum(a, dtype=np.int64))

# Tránh tràn số khi làm việc với số nguyên nhỏ.
```
**Ex4: Sử dụng where (tính tổng có điều kiện)**
```python
a = np.array([1, 2, 3, 4, 5])

print(np.sum(a, where=(a % 2 == 0))) # Chỉ sum các số chẵn

# Kết quả
# 6
```
**Ex5: Tham số initial**
```python
print(np.sum(a, initial=10))

# Kết quả
# 25
# Tổng = 10 + (1+2+3+4+5)
```
**Ex6: Dùng out để lưu kết quả**
```python
result = np.zeros(1)
np.sum(a, out=result)
print(result)
```