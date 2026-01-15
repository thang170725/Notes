# norm()
```bash
- Thường được dùng để tính khoảng cách từ gốc tọa độ đến một danh sách các điểm trong không gian.
```
**Ex**
```python
import numpy as np

# Tạo một mảng chứa tọa độ của 3 điểm: (3,4), (1,1), và (0,5)
points = np.array([
    [3, 4],
    [1, 1],
    [0, 5]
])

# Tính L2 norm (khoảng cách Euclidean) theo từng hàng (axis=1)
distances = np.linalg.norm(points, axis=1)

print("Các điểm:")
print(points)
print("\nKhoảng cách từ gốc tọa độ đến mỗi điểm:")
print(distances)
Các điểm:
[[3 4]
 [1 1]
 [0 5]]

Khoảng cách từ gốc tọa độ đến mỗi điểm:
[5.         1.41421356 5.        ]
```