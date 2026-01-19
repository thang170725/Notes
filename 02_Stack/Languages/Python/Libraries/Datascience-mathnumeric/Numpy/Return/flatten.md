.flatten()
Để “làm phẳng” (chuyển từ mảng nhiều chiều → mảng 1 chiều).
Cú pháp:
array.flatten(order='C')
    • order='C': duyệt theo hàng (row-major order — mặc định).
    • order='F': duyệt theo cột (column-major order — kiểu Fortran).
arr = np.array([[1, 2, 3],
                [4, 5, 6]])

flat1 = arr.flatten(order='A')
flat2 = arr.flatten(order='C')
flat3 = arr.flatten(order='F')
flat4 = arr.flatten(order='K')
print(flat1, flat2, flat3, flat4)
[1 2 3 4 5 6] [1 2 3 4 5 6] [1 4 2 5 3 6] [1 2 3 4 5 6]
