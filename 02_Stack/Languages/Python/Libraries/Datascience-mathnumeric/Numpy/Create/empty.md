# empty
```bash
- Tạo mảng nhưng chưa quan tâm giá trị (nhanh nhất).
- np.empty không khởi tạo giá trị, trong mảng sẽ là số rác (rất nhanh).
- Dùng khi:
    + Bạn sẽ gán giá trị sau
    + Hiệu năng quan trọng
```
**Syn**
```bash
import numpy as np

arr = np.empty((h, w))   # h, w là kích thước đã biết
```