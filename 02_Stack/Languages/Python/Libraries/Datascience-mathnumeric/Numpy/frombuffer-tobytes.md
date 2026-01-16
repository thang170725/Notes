# frombuffer
- Chuyển bytes → numpy array 1 chiều.
- Thường dùng kèm với cv2.imdecode
**Syn**
```bash
np.frombuffer(buffer, dtype=np.uint8, count=-1, offset=0)
```
**Ex**
```python
np_arr = np.frombuffer(image_bytes, np.uint8)
# np_arr = [137, 80, 78, 71, ...]
# CHƯA phải ảnh, chỉ là byte stream
```

# .tobytes()
Chuyển np.ndarray → bytes (gửi HTTP)
**Syn**
```bash
ndarray.tobytes(order='C')
```