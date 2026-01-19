zeros_like()
Để tạo một mảng mới có cùng hình dạng (shape) và kiểu dữ liệu (dtype) với mảng gốc, nhưng tất cả các phần tử đều bằng 0.
Cú pháp:
np.zeros_like(a, dtype=None)
    • a: mảng gốc muốn “bắt chước” shape và dtype.
    • dtype: (tuỳ chọn) nếu muốn đổi kiểu dữ liệu, có thể truyền thêm vào.
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.zeros_like(a)

print("a:\n", a)
print("b:\n", b)
a:
 [[1 2 3]
  [4 5 6]]
b:
 [[0 0 0]
  [0 0 0]]