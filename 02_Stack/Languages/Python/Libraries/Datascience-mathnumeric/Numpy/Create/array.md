# np.array()
```bash
- Để tạo mảng.
```
**Syn**
```bash
arr = np.array([1,2,3,4,5], dtype=float)

- dtype    : Trả về kiểu dữ liệu của mảng
```
**Ex**
```python
arr = np.array([1.2, 2, 3, 4])
print(arr.dtype) # Float64

arr = np.array([1, 2, 3, 4], dtype="S")
print(arr[0] + arr[1])
print(arr.dtype) # b'12'

arr = np.array([1, 2, 3, 4], dtype='i4') # i4 là kiểu dữ liệu integer có kích thước 4 bytes
print(arr)
print(arr.dtype)
[1 2 3 4]
int32
```