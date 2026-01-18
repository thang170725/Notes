# Tính khoảng cách 2 điểm trong không gian 2d
```python
import numpy as np

coordinates = np.array([
    [1,2],
    [3,4]
])

distance = np.linalg.norm(coordinates[0]-coordinates[1])
print(distance) # 2.8284271247461903
```