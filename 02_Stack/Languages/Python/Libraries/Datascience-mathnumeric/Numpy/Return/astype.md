# .astype()
```bash
- Dùng để chuyển kiểu dữ liệu của mảng sang kiểu khác.
```
**Syn**
```bash
a = array.astype(dtype)

- dtype: là kiểu dữ liệu bạn muốn chuyển sang, ví dụ: int, float, bool, str, np.int32, np.float64, …
```
**Ex1**
```python
arr = np.array([1.1, 2.1, 3.1])
newarr = arr.astype('i')
print(newarr) # [1 2 3]
print(newarr.dtype) # int32
```
**Ex2**
```python
arr = np.array([1.1, 2.1, 3.1])
newarr = arr.astype(int)
print(newarr) # [1 2 3]
print(newarr.dtype) # int64
```
**Ex3**
```python
arr = np.array([1, 0, 3])
newarr = arr.astype(bool)
print(newarr) # [ True False True]
print(newarr.dtype) # bool
```