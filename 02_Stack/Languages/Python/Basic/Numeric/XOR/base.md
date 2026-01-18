# ^ (XOR)
```bash
- Kết quả ĐÚNG (1) khi 2 toán hạng KHÁC nhau
- Kết quả SAI (0) khi 2 toán hạng GIỐNG nhau
```
**Formula**
```bash
A	B	A XOR B
0	0	0
0	1	1
1	0	1
1	1	0
```
**Property**
```bash
XOR có 3 tính chất cực quan trọng:
1. Tự triệt tiêu: a ^ a = 0
2. XOR với 0 giữ nguyên: a ^ 0 = a
3. XOR là phép TOÁN NGHỊCH ĐẢO (invertible): a ^ b = c  ⇔  c ^ a = b  ⇔  c ^ b = a
```
**Ex**
```python
print(1 ^ 1)  # 0
print(1 ^ 0)  # 1
print(0 ^ 1)  # 1
print(0 ^ 0)  # 0
```
**
**Ex2: XOR trên số nguyên (bitwise XOR)**
```python
a = 5   # 0101
b = 3   # 0011

print(a ^ b)

# Phân tích
#   0101  (5)
# ^ 0011  (3)
# ------
#   0110  (6)
# Kết quả: 6
```
4️⃣ XOR với boolean
print(True ^ False)  # True
print(True ^ True)   # False
print(False ^ False) # False


✔ Python cho phép XOR boolean trực tiếp

5️⃣ XOR với nhiều toán hạng
print(1 ^ 0 ^ 1)  # 0


Vì:

(1 ^ 0) ^ 1 = 1 ^ 1 = 0

6️⃣ Các tính chất QUAN TRỌNG của XOR (rất hay dùng)
6.1 XOR với chính nó → 0
a ^ a == 0

6.2 XOR với 0 → giữ nguyên
a ^ 0 == a

6.3 XOR có tính giao hoán & kết hợp
a ^ b == b ^ a
(a ^ b) ^ c == a ^ (b ^ c)

7️⃣ Ứng dụng XOR cực hay (phỏng vấn hay hỏi)
🔹 7.1 Tìm số xuất hiện 1 lần (các số khác xuất hiện 2 lần)
arr = [4, 1, 2, 1, 2]
result = 0
for x in arr:
    result ^= x

print(result)  # 4


👉 Vì:

a ^ a = 0
0 ^ b = b

🔹 7.2 Swap 2 biến KHÔNG cần biến tạm
a = 10
b = 20

a ^= b
b ^= a
a ^= b

print(a, b)  # 20 10

🔹 7.3 Toggle (bật / tắt) cờ bit
flag = 0b1010
mask = 0b0010

flag ^= mask
print(bin(flag))

8️⃣ XOR với NumPy (bonus)
import numpy as np

a = np.array([1, 0, 1, 0])
b = np.array([0, 1, 1, 0])

print(a ^ b)


👉 Kết quả:

[1 1 0 0]

9️⃣ Phân biệt XOR với OR & AND
Toán tử	Ký hiệu	Khi nào TRUE
AND	&	cả hai đúng
OR	`	`
XOR	^	chỉ một đúng
🔟 Tóm tắt nhanh

✔ XOR trong Python dùng ^
✔ XOR = khác thì 1, giống thì 0
✔ Là bitwise operator
✔ Rất mạnh trong xử lý bit, thuật toán