# Series
```bash
- Là mảng một chiểu giống như Numpy, hay là một cột của một bảng, nhưng nó thêm một cột đánh số thứ tự. 
- Series có thể được khởi tạo thông qua Numpy, dict hoặc các dữ liệu vô hướng bình thường. 
- Series có nhiều thuộc tính. Bạn có thể chuyển đổi Series sạng dạng dtype xác định, tạo bảng copy, trả về dạng bool của một thành phần.
```
**Ex**
```python
s = pd.Series([0,1,2,3], index=["a","b","c","d"])

# a    0
# b    1
# c    2
# d    3
# dtype: int64
```