M
filter()
Dùng để lọc các phần tử trong một iterable (như danh sách, tuple, …) dựa trên một điều kiện mà bạn xác định thông qua một hàm trả về giá trị True/False.
Cú pháp: filter(function, iterable)
numbers = [5,2,9,1,7,6,8,3,4]
m = filter(lambda n:n%2 == 0, numbers)
print(list(m))
[2, 6, 8, 4]
