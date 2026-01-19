```bash
- Là thư viện toán học, tính toán mạnh về mảng nhiều chiều, vector. 
- pip install numpy. import numpy as np
```

# .ndim
Trả về một số nguyên cho chúng ta biết mảng có bao nhiêu chiều.
**Ex**
```python
arr = np.array((1,2,3))
print(arr.ndim) # 1
```


# .tolist()
Để chuyển từ mảng numpy sang mảng thường.
**Cú pháp**
```text
arr.tolist()
```






.ndmin
Xác định số chiều của mảng.
Cú pháp:
import numpy as np
arr = np.array([1, 2, 3, 4], ndmin=2)
print(arr)
print('number of dimensions :', arr.ndim)
[[1 2 3 4]]
number of dimensions : 2
.mean()
import numpy as np
a = np.array([1,2,3,4]).mean()
print(a)
2.5

Asarray()
Dùng để chuyển dữ liệu bất kỳ (list, tuple, list lồng nhau, …) thành mảng NumPy (ndarray) nhưng không tạo bản sao (copy) nếu không cần thiết — tức là nếu đầu vào đã là ndarray rồi thì nó trả về chính nó, không tạo mảng mới.
Cú pháp:
arr = np.asarray(lst, dtype=float)
import numpy as np

arr1 = np.array([1, 2, 3])
arr2 = np.asarray(arr1)

print(arr1 is arr2)  # True -> cùng vùng nhớ
np.asarray() không tạo copy → tiết kiệm bộ nhớ.



*
Phép nhân từng phần tử.
Cú pháp:
arr = np.array([[5, 10], [1,2]], dtype=float)
arr1 = np.array([[2, 3], [1,2]], dtype=float)
print(arr*arr1)
[[10. 30.]
 [ 1.  4.]]



Clip()
Để giới hạn giá trị của các phần tử trong mảng trong một khoảng nhất định.
Cú pháp:
np.clip(array, min_value, max_value)
    • array: Mảng cần xử lý
    • min_value: Giá trị nhỏ nhất cho phép
    • max_value: Giá trị lớn nhất cho phép
a = np.array([-5, 0, 5, 10, 15, 20])
clipped = np.clip(a, 0, 10)
print(clipped) # [0 0 5 10 10 10]
Dot()
Để nhân ma trận. 1 chiều hoặc n chiều
Cú pháp:
a = np.array([
    [1,2,3],
    [1,1,1],
    [2,3,4]
])
b = np.array([
    [2,2,2],
    [1,2,3],
    [4,3,1]
])
res = np.dot(a,b)
print(res)
[[16 15 11]
 [ 7  7  6]
 [23 22 17]]



Để tính e mũ n
Cú pháp:
np.exp(2) # e**2
@ || matmul()
Gần giống như dot đều thực hiện nhân ma trận chuẩn, nhưng mảng >2D (tensor) thì dot không hỗ trợ tốt, còn @, matmul hỗ trợ broadcasting – Tốt.
Random
Rand()
Dùng để sinh số ngẫu nhiên trong khoảng [0, 1). Theo phân phối đều.
Cú pháp:
    1. np.random.rand() # sinh ngẫu nhiên 1 số
    2. np.random.rand(5) # sinh ngẫu nhiên 1 mảng 5 số
    3. np.random.rand(3,4) # sinh ngẫu nhiên mảng 2 chiều 3x4
    4. 10 + (20-10)*np.random.rand(10)) # sinh ngẫu nhiên số từ 10 đến 20
Randint()
Tạo ra số nguyên ngẫu nhiên trong một khoảng xác định.
Cú pháp:
 np.random.randint(low, high=None, size=None, dtype=int)
    • low: Giá trị nhỏ nhất.
    • high: Giá trị lớn nhất.
    • size: int hoặc tuple, là kích thước của mảng.
    • dtype: Kiểu dữ liệu.
r = np.random.randint(1, 10, size=5)
print(r)
[6 4 6 3 3]
r = np.random.randint(1, 10, size=(5,5))
print(r)
[[2 1 5 4 2]
 [9 7 1 2 5]
 [4 4 7 9 6]
 [7 4 4 1 6]
 [9 7 2 2 7]]
Uniform()
Thường dùng để tạo ra các tập dữ liệu lớn để thử nghiệm (tập dữ liệu ngẫu nhiên ở bất kỳ kích thước nào).
Cú pháp:
color = np.random.uniform(0, 1, size=(100, 3))
    • 0: số bắt đầu
    • 1: số kết thúc
    • size: kích thước
number = np.random.uniform(0, 10, 5) # tạo ra 5 số từ 0 - 10
print(number)
[5.20684506 5.6623642  3.70489081 1.98964972 0.14884213]
seed()
randn()
Được dùng để tạo ra số ngẫu nhiên tuân theo quy luật phân phối chuẩn với trung bình (mean) = 0 và độ lệch chuẩn = 1.
Cú pháp: np.random.randn(d0, d1, …, dn)
normal()
Tạo một mảng giá trị ngẫu nhiên, trong đó các giá trị tập trung xung quanh một giá trị cho trước. Loại phân phối dữ liệu này được gọi là phân phối dữ liệu chuẩn hoặc phân phối dữ liệu gauss.
Cú pháp: 
numpy.random.normal(loc=0.0,  size=None, scale=1.0)
    • loc: Trung bình (mean) của phân phối.
    • scale: Độ lệch chuẩn của phân phối.
    • size: kích thước của mảng kết quả có thể là số nguyên, tuple, hoặc None).
number = np.random.normal(0.0, scale=10, size=50)
plt.hist(number, bins=10)
plt.show()



binomial()
    • Dùng để sinh ra các giá trị ngẫu nhiên theo phân phối nhị thức (binomial distribution).
    • Phân phối nhị thức mô tả số lần thành công trong một số lần thử cố định, với xác suất thành công không đổi trong mỗi lần thử.
    • Ứng dụng là mô phỏng thử nghiệm Bernoulli lặp lại nhiều lần, tạo dữ liệu giả lập cho bài toán phân loại nhị phân. Mô phỏng kết quả của thí nghiệm có xác suất (sổ xố, trò chơi, …)
Cú pháp: numpy.random.binomial(n, p, size=None)
    • n: Số lần thử (Số nguyên dương)
    • p: Xác suất thành công trong mỗi lần thử (0 <= p <= 1)
    • size: Số lượng giá trị random muốn tạo ra (có thể là một số nguyên hoặc tuple, ví dụ (3, 3)
import numpy as np
result = np.random.binomial(n=10, p=1/6, size=5)
print(result)
# xác suất xuất hiện mặt 6 chấm khi tung 5 lượt mỗi lượt lại tung 10 lần
[2 3 6 2 1]
choice()
Là một hàm trong Python được sử dụng để chọn một phần tử ngãu nhiên từ một chuỗi (ssequence) cho trước. Chuỗi này có thể là.
    • Danh sách (list): Một tập hợp các phần tử có thứ tự, có thể thay đổi.
    • Tuple: Một tập hợp các phần tử có thứ tự, không thể thay đổi.
    • Chuỗi ký tự (string): Một dãy các ký tự.
argsort()
Trả về chỉ số các phần tử được sắp xếp theo cách tăng dần.
bincount()
Log2()

Concatenate
Stack
Hstack
Vstack
Split
Array_split
var()
Để tìm phương sai.
Phương sai là một số đo cho biết mức độ phân tán của các giá trị trong tập dữ liệu so với giá trị trung bình của tập dữ liệu đó. Phương sai cho biết các giá trị trong tập dữ liệu “lan rộng” ra sao xung quanh giá trị trung bình.
Phương sai càng lớn thì giá trị trong tập dữ liệu càng phân tán xa so với giá trị trung bình và ngược lại.
import numpy as np
def main():
    value = [12,34,45,70,86]
    print(np.var(value))
main()
683.8399999999999
# trả về phương sai tổng thể
percentile()
Để tìm phần trăm thứ n.
Ý tưởng: 
    1. Sắp xếp mảng tăng dần
    2. index = (q/100) * (n-1)
    3. Nội suy: <value> = <value0> + (<value1> – <value0>) * (index – floor(index))
value0 = 10, value1 = 20
Ví dụ: [60,40,50,30,20,10] – Tìm phần trăm thứ 12
    1. Sắp mảng tăng dần: [10,20,30,40,50,60]
    2. index = (12/100) * (6-1) = 0.6
    3. Nội suy: value = 10 + (20-10) * (0.6 – 0) = 16
Code:
import numpy as np
import math
def main():
    ages = [60,40,50,30,20,10]
    x = np.percentile(ages, 12)
    print(x)
main()
16.0
maximum()
import numpy as np
a = np.maximum(0,2)
print(a)
2
polyfit()
Được dùng để khớp một đa thức với một tập dữ liệu. Hàm này rất hữu ích trong việc tim ra mối quan hệ giữa các biến và dự đoán các giá trị trong tương lai.
Cú pháp: numpy.polyfit(x, y, deg, rcond = None, full = False, w = None, cov = False)
    • x: Mảng các tọa độ x của các điểm dữ liệu.
    • y: Mảng các tọa độ y của các điểm dữ liệu.
    • deg: Bậc của đa thức cần khớp
    • full: Nếu là True, hàm này sẽ trả về thêm thông tin về phép khớp.
    • w: Mảng trọng số áp dụng cho các điểm dữ liệu.
    • cov: Nếu là True, hàm này sẽ trả về ma trận hiệp phương sai của các hệ số.
Tham số đầu ra:
Trả về một mảng các hệ số của đa thức đã khớp. Nếu full = True, hàm này sẽ trả về một tuple chứa các hệ số, phần dư bình phương, hạng của ma trận Vandermonde và các giá trị riêng của ma trận hiệp phương sai.
import numpy as np
def main():
    x = [1, 3, 5, 6, 7, 8, 9, 10, 12, 13, 14, 15, 16, 18, 19, 21, 22, 23]
    y = [100, 90, 80, 60, 60, 55, 60, 65, 70, 70, 75, 76, 78, 79, 90, 99, 99, 100]

    print(np.polyfit(x, y, 2))
main()
[ 0.29363675 -6.34185897 99.32921645]
Tìm hệ số của phương trình bậc 2 khi biết 10 điểm
import numpy as np
def main():
    x = [1,2,3,4,5,6,7,8,9,10]
    y = [0,6,14,24,36,50,66,84,104,126]
    print(np.polyfit(x, y, 2))
main()
[ 1.  3. -4.]
poly1d()
Để biểu diễn 1 đa thức một chiều, lớp này cung cấp các phương thức để thực hiện các phép toán trên đa thức, chẳng hạn như tính giá trị đa thức tại một điểm, tính đạo hàm và tính tích phân của đa thức.
Cú pháp: numpy.poly1d(c_or_r, r = False, variable = None)
    • c_or_r: Mảng các hệ số của đa thức, theo thứ tự giảm dần của bậc, Hoặc, nếu r = True, thì đây mảng các nghiệm của đa thức.
    • r: Nếu là True, c_or_r được hiểu là mảng các nghiệm của đa thức.
    • variable: Chuỗi ký tự tự biểu diễn biến của đa thức. Mặc định là “x”.
import numpy as np
def main():
    x = [1,2,3,4,5,6,7,8,9,10]
    y = [0,6,14,24,36,50,66,84,104,126]
    # đa thức bậc 2
    res = np.poly1d(np.polyfit(x, y, 2))
    # res trả về kế quả là một đa thức bậc 2
    # res = x^2 + 3x - 4
    print(res)
    # 2^2 + 3*2 - 4 = 6
    print(res(2))
main()
   2
1 x + 3 x – 4
5.99999999999999
linspace()
Để tạo một mảng số cách đều nhau trên một khoảng xác định.
Cú pháp: numpy.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None, axis=0)
    • start: Giá trị bắt đầu của dãy số.
    • stop: Giá trị kết thúc của dãy số.
    • num: Số lượng phần tử trong dãy số (mặc định là 50).
    • endpoint: Nếu là True (mặc định), stop là phần tử cuối cùng của dãy số. Nếu là false, stop không được bao gồm.
    • retstep: Nếu là True, hàm này trả về một tuple gồm mảng và khoảng cách giữa các phần tử.
    • dtype: Kiểu dữ liệu của các phần tử trong mảng.
    • axis: Trục để lưu kết quả.
import numpy as np
def main():
    res = np.linspace(0, 10, num=10, endpoint=False)
    print(res)
main()
[0. 1. 2. 3. 4. 5. 6. 7. 8. 9.]
deriv()
integ()
Log()
L


column_stack()
Bài tập
Đếm số điểm nằm trong một hình tròn và giá trị pi
Giả sử bạn muốn tính xấp xỉ giá trị π bằng phương pháp Monte Carlo:
– Sinh ngẫu nhiên N điểm trong hình vuông [-1, 1] × [-1, 1]
– Đếm bao nhiêu điểm nằm trong đường tròn bán kính 1
– π ≈ 4 * (số điểm trong hình tròn / tổng số điểm)
import numpy as np

# Tổng số điểm
N = 1_000_000  # 1 triệu điểm

# Sinh ngẫu nhiên (x, y) trong [-1, 1]
x = np.random.uniform(-1, 1, N)
y = np.random.uniform(-1, 1, N)

# Đếm số điểm nằm trong đường tròn
inside = (x**2 + y**2) <= 1
count_inside = np.sum(inside)

# Tính tỉ lệ và xấp xỉ pi
pi_estimate = 4 * count_inside / N

print(f"Số điểm trong đường tròn: {count_inside}")
print(f"Xấp xỉ π = {pi_estimate}")
