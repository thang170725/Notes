Vòng lặp
Là cấu trúc lặp. ctrl+C để thoát khỏi vòng lặp vô hạn.


Cú pháp:
while <condition>:
	statement
number = int(input("Nhập số nguyên: "))
result = ""
while number > 0:
    remainder = number%2
    result += str(remainder)
    number //= 2
print(result[::-1])
Nhập số nguyên: 524
1000001100
Range()
Là cấu trúc vòng lặp dạng basic.
Cú pháp:
    • range(start, stop, step)
    • range(start,  stop)
a = [1,2,3,4,5]
for i in range(0,len(a)):
    print(a[i])
1
2
3
4
5
for i in range(5,1,-1):
    print(i)
5
4
3
2
str = str(input("Nhập chuỗi nhị phân: "))
sum = 0
for i in range(0, len(str)):
    sum += int(str[i])*pow(2, len(str)-i-1)
print(sum)
Nhập chuỗi nhị phân: 1010101100
684
a = list(range(1, 6))
[1,2,3,4,5]
a = [i for i in range(1, 6)]
[1,2,3,4,5]

enumrate()
Để duyệt qua một chuỗi như danh sách, tuple, chuỗi ký tự, … Đồng thời lấy ra các số index và giá trị của từng phần tử trong chuỗi.
Cú pháp: enumerate(fruits, start=1)
fruits = ["táo", "chuối", "cam"]
for index, fruit in enumerate(fruits):
    print(f"Trái cây thứ {index + 1} là {fruit}")
Trái cây thứ 1 là táo
Trái cây thứ 2 là chuối
Trái cây thứ 3 là cam

