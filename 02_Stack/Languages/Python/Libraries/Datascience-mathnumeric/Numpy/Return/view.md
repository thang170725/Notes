.view()
Tạo một chế độ xem focus vào mảng gốc.
Cú pháp:
arr = np.array([1, 2, 3, 4, 5])
x = arr.view()
arr[0] = 42
print(arr)
print(x)
[42 2 3 4 5]
[42 2 3 4 5]