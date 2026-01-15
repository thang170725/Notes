Import thư viện math
import math

2. Các hằng số trong math
math.pi     # số Pi ≈ 3.14159
math.e      # số e ≈ 2.71828

Ví dụ
r = 3
area = math.pi * r * r
print(area)


👉 Tính diện tích hình tròn

3. Làm tròn số
math.floor() – làm tròn xuống
math.floor(3.7)   # 3

math.ceil() – làm tròn lên
math.ceil(3.2)    # 4

math.trunc() – cắt phần thập phân
math.trunc(3.9)   # 3


📌 Đời thường:

floor → xuống đất

ceil → lên trần

4. Căn bậc hai & lũy thừa
Căn bậc hai
math.sqrt(16)     # 4.0

Lũy thừa
math.pow(2, 3)    # 8.0


📌 So sánh:

2 ** 3            # 8 (toán tử Python)

5. Giá trị tuyệt đối & dấu
Trị tuyệt đối
math.fabs(-5.3)   # 5.3

Kiểm tra dấu
math.copysign(5, -1)  # -5.0

6. Logarithm
Log cơ số e
math.log(10)

Log cơ số 10
math.log10(100)   # 2.0

Log cơ số 2
math.log2(8)      # 3.0

7. Hàm lượng giác (đơn vị là RADIAN ⚠️)
Sin / Cos / Tan
math.sin(math.pi / 2)   # 1.0
math.cos(0)             # 1.0
math.tan(math.pi / 4)   # 1.0

Đổi độ ↔ radian
math.radians(90)   # độ → radian
math.degrees(math.pi)  # radian → độ

8. So sánh & kiểm tra đặc biệt
So sánh số thực an toàn
math.isclose(0.1 + 0.2, 0.3)  # True

Kiểm tra vô cực / NaN
math.isinf(10**1000)   # True
math.isnan(float('nan'))  # True

9. GCD & LCM (hay dùng)
Ước chung lớn nhất
math.gcd(12, 18)   # 6

Bội chung nhỏ nhất (Python 3.9+)
math.lcm(4, 6)     # 12

10. Ví dụ tổng hợp dễ nhớ
import math

a = 5
b = 2

print(math.sqrt(a))
print(math.pow(a, b))
print(math.ceil(3.4))
print(math.floor(3.9))
print(math.sin(math.radians(30)))

11. Những hàm nên nhớ nhất cho người mới ⭐
Nhóm	Hàm
Làm tròn	floor, ceil
Căn & mũ	sqrt, pow
Hằng số	pi, e
Lượng giác	sin, cos
So sánh	isclose
Toán số	gcd, lcm
Tóm lại 1 câu

📦 math = các công cụ toán học chính xác, chuẩn, dễ dùng
Math
sqrt()
Để lấy căn bậc 2 của một số.. Thư viện math không cần tải về mà có thể import trực tiếp.
Cú pháp: math.sqrt(value)
import math
a = math.sqrt(36)
print(a)
6.0
floor()
Để làm tròn số (chỉ lấy phần nguyên).
import math
def main():
    print(math.floor(3.3), math.floor(3.7))
main()
3 3
pow()
Để lấy giá trị mũ của một số. 
Cú pháp: math.pow(x, n)
log2()
import math

x = 8
print(math.log2(x))  # 3.0
