.copy()
Để sao chép một mảng.
Cú pháp:
arr = np.array([1, 2, 3, 4, 5])
x = arr.copy()
arr[0] = 42
print(arr)
print(x)
[42 2 3 4 5]
[1 2 3 4 5]