- [Nhập tên (Dữ liệu dạng chữ)](#nhập-tên-dữ-liệu-dạng-chữ)
- [Nhập số và thực hiện phép tính (Ép kiểu)](#nhập-số-và-thực-hiện-phép-tính-ép-kiểu)
- [Nhập nhiều giá trị trên một dòng](#nhập-nhiều-giá-trị-trên-một-dòng)
- [Nhập ma trận (nxm)](#nhập-ma-trận-nxm)
- [Tạo ra dict lưu tọa độ n điểm](#tạo-ra-dict-lưu-tọa-độ-n-điểm)

---

# Nhập tên (Dữ liệu dạng chữ)
```bash
Đây là cách dùng cơ bản nhất để lấy thông tin văn bản.
```
```python
ten = input("Chào bạn, bạn tên là gì? ")
print("Rất vui được gặp bạn, " + ten + "!")
```

# Nhập số và thực hiện phép tính (Ép kiểu)
```bash
Vì input() trả về chuỗi, nên nếu bạn muốn tính toán, bạn phải ép kiểu nó sang số nguyên (int) hoặc số thực (float).
```
```python
nam_sinh_str = input("Bạn sinh năm bao nhiêu? ") # Nhập năm sinh
nam_sinh = int(nam_sinh_str) # Chuyển đổi từ chuỗi sang số nguyên để tính toán

tuoi = 2026 - nam_sinh
print(f"Vậy là năm nay bạn {tuoi} tuổi rồi!")
```

# Nhập nhiều giá trị trên một dòng
```bash
Đôi khi bạn muốn người dùng nhập nhiều thông tin cùng lúc (ví dụ: họ và tên cách nhau bởi dấu cách), bạn có thể dùng phương thức .split().
```
```python
ho, ten = input("Nhập Họ và Tên của bạn (cách nhau bởi dấu cách): ").split()
print(f"Họ của bạn là: {ho}")
print(f"Tên của bạn là: {ten}")
```

# Nhập ma trận (nxm)
```bash
2 3
1 2 3
4 5 6
```
**Ex1**
```python
# Nhập số hàng và số cột
n, m = map(int, input().split())

# Nhập ma trận
a = []
for _ in range(n):
    row = list(map(int, input().split()))
    a.append(row)

for row in a:
    print(*row)
```
**Ex2**
```python
n, m = map(int, input().split())
a = [list(map(int, input().split())) for _ in range(n)]

for row in a:
    print(*row)
```

# Tạo ra dict lưu tọa độ n điểm
**Topic**
```bash
Nhập vào tọa độ n điểm và lưu các tọa độ đó vào một dict
```
**Answer**
```python
n = int(input("Number of points: "))

print("=== Ex: A(x1, y1) ====")
coordinates = [input().strip() for _ in range(n)]

local_coordinates = {}

for c in coordinates:
    name, rest = c.split("(", 1)
    x, y = rest.rstrip(")").split(",")

    local_coordinates[name.strip()] = (int(x), int(y))

print(local_coordinates)

# Number of points: 2
# === Ex: A(x1, y1) ====
# A(1,2)
# B(3,6)
# {'A': (1, 2), 'B': (3, 6)}
```