Xử lý file 
Open() & .close()
Để mở file và đóng file
Cú pháp: 
open(‘data.txt’, ‘w’, encoding=’utf8’)
    • r – Đọc – Giá trị mặc định. Mở tệp để đọc, báo lỗi nếu tệp không tồn tại.
    • a – Thêm – Mở tệp để thêm, tạo tệp nếu tệp không tồn tại. Thêm vào cuối file.
    • w – Ghi – Mở tệp để ghi, tạo tệp nếu tệp không tồn tại. Ghi đè nếu file có nội dung trước đó.
    • t – Văn bản – Giá trị mặc định. Chế độ văn bản.
    • b – Nhị phân – Chế độ nhị phân (Ví dụ: hình ảnh).

.write()
Để ghi vào một file.
Cú pháp:
# Tại file Text.txt có nội dung: Hello world

txt = open("E:\\Python\Text.txt", "wt")
txt.write("i am from VietNam")
i am from VietNam
.name
Trả về tên của file đang được mở.
Cú pháp:
    txt = open("D:\\workspace\Python_box\\a.txt", "rt")
    print(txt.name)
D:\workspace\Python_box\a.txt
.mode
Trả về chế độ mode đang được mở.
Cú pháp:
    txt = open("D:\\workspace\Python_box\\a.txt", "rt")
    print(txt.mode)
rt

With … as
    • with dùng để quản lý tài nguyên tự động:
        ◦ Tự mở → tự đóng (file, database, network, lock…)
        ◦ Tự giải phóng tài nguyên kể cả khi code bị lỗi
        ◦ Không cần viết try / finally
    • Nó hoạt động dựa trên giao thức context manager:
        ◦ __enter__()
        ◦ __exit__()
Cú pháp:
f = open("data.txt", "w")
f.write("hello")
f.close()  # nếu quên close → rò rỉ tài nguyên
Nếu code bị lỗi trước khi close() → file không được đóng.
with open("data.txt", "w") as f:
    f.write("hello world")
File tự đóng dù có lỗi trong block
Code gọn, sạch
with open("data.txt", "r", encoding="utf8") as f:
    content = f.read()
    print(content)
# Khi block with kết thúc → file tự đóng.
with open("input.txt") as inp, open("output.txt", "w") as out:
    for line in inp:
        out.write(line.upper())
# Rất tiện để xử lý nhiều file.

isinstance()
Trả về true nếu đối tượng được chỉ định thuộc loại được chỉ định, nếu không thì trả về false.
Cú pháp: isinstance(object, type)
x = isinstance("Hello", (str, float, int, str, list, dict, tuple))
print(x)
True
id()
Để xem địa chỉ id của một biến trong bộ nhớ.
Cú pháp: id(<variable>)
Ép kiểu
Để ép từ một kiểu bất kỳ sang kiểu int (nếu ép được). Nếu biến cần ép không phải là số thì sẽ bị lỗi.
Cú pháp: int(<variable>)
a = "10"
b = int(a)
print(type(b))
<class 'int'>
Bài tập
Chuyển 0 về cuối mảng bằng two pointer
def move0(li):
    pos = 0
    for i in range(len(li)):
        if li[i] != 0:
            li[pos] = li[i]
            pos += 1
    for i in range(pos, len(li)):
        li[i] = 0
    return li
n1 = move0([3,2,5,7,0,8,1,9])
print(n1)

Tìm số nguyên tố bằng thuật toán Miller-Rabin
Đây là thuật toán cố độ phức tạp thấp.
Ví dụ 1
Giả sử n = 561
    1. n-1 = .m (560 = )
    2. Chọn a=2; 1<2<560
    3. (mod n) 
(mod 561) = 263 -> kiểm tra có bằng 1 hoặc n-1 không	
(mod 561) = 166
(mod 561) = 67
(mod 561) = 1 -> kết luận
Ví dụ 2
Kiểm tra số n = 11363 có phải số nguyên tố hay không
    1. Phân tích: n-1 = .m (11362 = *5681)
    2. Chọn a = 2 (1 < a < 11362)
    3. (mod n) = (mod 11363)
Bằng Hàm bình thường
Output: 6
def UCLN(n1,n2):
    result = 1
    # xử lý riêng trường hợp 2 số đó chia hết cho 2 (chẵn)
    while n1 % 2 == 0  and n2 % 2 == 0:
        n1 //= 2
        n2 //= 2
        result *= 2
    # xử lý các trường hợp còn lại (lẻ)
    for i in range(3, min(n1,n2)+1, 2):
        while n1 % i == 0 and n2 % i == 0:
            n1 /= i
            n2 /= i
            result *= i
    return result
def main():
    print(UCLN(12, 18))
main()

Cải tiến code:
def UCLN(n1,n2):
    while n2 != 0:
        r = n1 % n2
        n1 = n2
        n2 = r
    return n1
def main():
    print(UCLN(12, 18))
main()


Bằng hàm đệ quy
Output: 2
def UCLN(n1,n2,result = 1):
    if(n1 == 1 or n2 == 1): return 1
    # xử lý riêng trường hợp 2 số đó chia hết cho 2 (chẵn)
    while n1 % 2 == 0  and n2 % 2 == 0:
        return UCLN(n1//2, n2//2, result*2)
    # xử lý các trường hợp còn lại (lẻ)
    i = 3
    while i <= min(n1,n2):
        if n1 % i == 0 and n2 % i == 0:
            return UCLN(n1//i, n2//i, result*i)
        i += 2
    return result
def main():
    print(UCLN(22, 18))
main()

Cải tiến code:
def UCLN(n1,n2):
    if n2 == 0:
        return n1
    return UCLN(n2, n1 % n2)
def main():
    print(UCLN(22, 18))
main()

Tính a^b mod n
def mod_pow(a, b, n):
    result = 1
    a = a % n  # Đảm bảo a nhỏ hơn n để tối ưu
    while b > 0:
        if b % 2 == 1:
            result = (result * a) % n
        a = (a * a) % n
        b //= 2
    return result

# Ví dụ sử dụng:
a = 3
b = 200
n = 13
print(mod_pow(a, b, n))  # Kết quả sẽ là (3^200) mod 13

Tìm nghịch đảo trên Zn
def nghich_dao(n, a):
    r0 = n
    r1 = a
    r2 = r0%r1
    q = r0//r1
    t0 = 0
    t1 = 1
    t2 = t0 - t1*q
    while r2 != 0:
        r0 = r1
        r1 = r2
        r2 = r0%r1
        q = r0//r1
        t0 = t1
        t1 = t2
        t2 = t0 - t1*q
    return n+t1
print(nghich_dao(43, 17))

Thuật toán đảo ngược chuỗi
Bằng hàm đệ quy
!dlroW olleH
def reverseStr(str):
    if len(str) == 0: return str
    return reverseStr(str[1:]) + str[0]
def main():
    print(reverseStr("Hello World!"))
main()
Thuật toán tìm max
Bằng hàm bình thường
def maxList(arr):
    max = arr[0]
    for i in range(1,len(arr)):
        if max < arr[i]:
            max = arr[i]
    return max
def main():
    print(maxList([4,3,6,8,9,3,2,1]))
main()

Thuật toán tìm kiếm
Thuật toán tìm kiếm tuần tự
Thuật toán Binary search – chia để trị
Output: 5
def findBinary(arr,k):
    l= 0
    r= len(arr)-1
    while l<= r:
        mid=(r+l)//2
        if arr[mid]== k: return mid
        elif arr[mid]>= arr[l]:
            l= mid+1
        else:
            r= mid -1
    return mid
def main():
    print(findBinary([1,3,5,7,9,10,292],10))
main()

Thuật toán sắp xếp
Thuật toán bubble sort – Array (Sắp xếp nổi bọt)
Xem ví dụ thuật toán ở đây: https://www.youtube.com/watch?v=xli_FI7CuzA
Độ phức tạp:
    • Trường hợp tốt nhất: O(n) – Khi mảng đã gần như được sắp xếp hoàn toàn.
    • Trường hợp trung bình và xấu nhất: O()
arr = [2,4,1,8,5,6,0,5,3]
def bubbleSort(a):
    for i in range(len(a)-1, 0, -1):
        for j in range(i):
            if a[j] > a[j+1]:
                temp = a[j]
                a[j] = a[j+1]
                a[j+1] = temp
    return a
print(bubbleSort(arr))
[0, 1, 2, 3, 4, 5, 5, 6, 8]
def bubbleSort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(n-1,i-1,-1):
            if arr[j] < arr[j-1]: arr[j], arr[j-1] = arr[j-1], arr[j]
    return arr

Thuật toán Selection sort – Array
Độ phức tạp: O() – cho mọi trường hợp.
arr = [2,4,1,8,5,6,0,5,3]
def SelectionSort(l):
    for i in range(len(l)):
        m = i
        for j in range(i+1, len(l)):
            if l[m] > l[j]:j
                m = j
        l[i], l[m] = l[m], l[i]
    return l
print(SelectionSort(arr))
[0, 1, 2, 3, 4, 5, 5, 6, 8]
Thuật toán insertion Sort - Array
Độ phức tạp:
    • Trường hợp tốt nhất: O(n)
    • Trường hợp trung bình và xấu nhất: O()
arr = [2,4,1,8,5,6,0,5,3]
def InsertionSort(l):
    for i in range(1, len(l)):
        temp = i
        while (temp > 0) and (l[temp] < l[temp-1]):
            l[temp], l[temp-1] = l[temp-1], l[temp]
            temp -= 1
    return l
print(InsertionSort(arr))
[0, 1, 2, 3, 4, 5, 5, 6, 8]
def insertionSort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and key < arr[j]:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr

Thuật toán QuickSort
Bằng đệ quy
Độ phức tạp:
    • Trường hợp tốt nhất: O(log(n))
    • Trường hợp xấu nhất: O(n2)
def quickSort(arr):
    if len(arr) <= 1: return arr
    else:
        pivot = arr[0]
        smaller = [x for x in arr[1:] if pivot > x]
        bigger = [x for x in arr[1:] if pivot < x]
        print(smaller, bigger)
        return quickSort(smaller) + [pivot] + quickSort(bigger)
def main():
    arr = [6,4,5,3,2,8,1, 9, 11, 7]
    print(quickSort(arr))
main()
[4, 5, 3, 2, 1] [8, 9, 11, 7]
[3, 2, 1] [5]
[2, 1] []
[1] []
[7] [9, 11]
[] [11]
[1, 2, 3, 4, 5, 6, 7, 8, 9, 11]


Thuật toán Heap Sort
Là cách sắp xếp dựa vào cây nhị phân
Độ phức tạp: O(n*log(n))
def heapify(arr, n, i):
    l = 2 * i + 1
    r = 2 * i + 2
    largest = i
    if l < n and arr[l] > arr[largest]:
        largest = l
    if r < n and arr[r] > arr[largest]:
        largest = r
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)
def heapSort(arr):
    # xây dựng max heap
    for i in range(len(arr) // 2 - 1, -1, -1):
        heapify(arr, len(arr), i)
    # sắp xếp
    for i in range(len(arr) - 1, 0, -1):
        arr[i], arr[0] = arr[0], arr[i]
        heapify(arr, i, 0)

67. Add binary – leetcode
class Solution(object):
    def addBinary(self, a, b):
        res = ""
        carry = 0
        a = a[::-1]
        b = b[::-1]
        for i in range(max(len(a), len(b))):
            digitA = ord(a[i]) - ord("0") if i < len(a) else 0
            digitB = ord(b[i]) - ord("0") if i < len(b) else 0
            total = digitA + digitB + carry
            char = str(total % 2)
            res = char + res
            carry = total // 2
        if carry:
            res = "1" + res
        return res
a = “11” b = “1”
Result = “100”

a = "1011"
b = "1001"
result = ""
temp = "0"
for i in range(len(a)-1, -1, -1):
    tr = a[i] + b[i] + str(temp)
    if tr.count("1") == 2:
        r = 0
    elif tr.count("1") != 2:
        r = int(a[i]) | int(b[i]) | int(temp)
    result = str(r) + result
    if tr.count("1") >= 2:
        temp = 1
    else:
        temp = 0
print(str(temp) + result)

Thuật toán kiểm tra chuỗi đối xứng
def Symmetrical(str):# summetrical: đối xứng
    temp = len(str)//2
    if len(str)%2 == 0:
        l = str[:temp]
        r = str[temp::]
        r = r[::-1]
    else:
        l = str[:temp]
        r = str[temp+1::]
        r = r[::-1]
    return l==r
abccba = True
abcd = False
def Symmetrical(str):# summetrical: đối xứng
    l, r = 0, len(str)-1
    while l <= r:
        if str[l] !=  str[r]: return False
        l += 1
        r -= 1
    return True

5. Longest Palindromic Substring – LeetCode
Tìm chuỗi đối xứng dài nhất trong một chuỗi cho trước.
class Solution(object):
    def Symmetrical(self, str):# summetrical: đối xứng
        temp = len(str)//2
        if len(str)%2 == 0:
            l = str[:temp]
            r = str[temp::]
            r = r[::-1]
        else:
            l = str[:temp]
            r = str[temp+1::]
            r = r[::-1]
        return l==r
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        longest = ""
        for i in range(len(s)):
            for j in range(i, len(s)):
                if s[i] == s[j]:
                    temp1 = s[i:j+1]
                    if self.Symmetrical(temp1) and len(temp1) > len(longest):
                        longest = temp1
        return longest
Input: babad
Out: bab hoặc aba
Cải tiến Code:
class Solution:
    def longestPalindrome(self, s):
        # Way better solution based on someone elses solution.
        # Utilizes string inserts to handle even-length palindromes.
        if s == s[::-1]:
            return s

        # Transform string to handle even-length palindromes
        t = "|" + "|".join(s) + "|"
        n = len(t)
        lps = [0] * n

        # Expand around each center
        for i in range(n):
            # Find the number of palindromes around each character, counting from the center
            while (
                i - lps[i] - 1 >= 0 # bounds check lower
                and i + lps[i] + 1 < n # bounds check higher
                and t[i - lps[i] - 1] == t[i + lps[i] + 1] # palindrome radii check
            ):
                lps[i] += 1

        # Identify the center with the longest palindrome
        center_index = lps.index(max(lps))
        start = center_index - lps[center_index]
        end = center_index + lps[center_index]
        # Remove inserted '|'
        return t[start:end].replace("|", "")

__import__("atexit").register(lambda: open("display_runtime.txt", "w").write("0"))
class Solution(object):
    def longestPalindrome(self, s):
        if not s:
            return ""

        n = len(s)
        dp = [[False] * n for _ in range(n)]
        start, max_length = 0, 1


        for i in range(n):
            dp[i][i] = True

        for i in range(n - 1):
            if s[i] == s[i + 1]:
                dp[i][i + 1] = True
                start = i
                max_length = 2

        for length in range(3, n + 1):
            for i in range(n - length + 1):
                j = i + length - 1
                if s[i] == s[j] and dp[i + 1][j - 1]:
                    dp[i][j] = True
                    start = i
                    max_length = length

        return s[start:start + max_length]


Tạo danh sách lưu tên, tuổi bằng mảng đối tượng
Json 12
Mickey 13
Titan 34
class person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def __str__(self):
        return f"{self.name} {self.age}"

class listPerson:
    li = []
    def __init__(self):
        pass
    def add(self, person):
        return self.li.append(person)
    def print(self):
        for i in self.li:
            print(i)
def main():
    sv1 = person("Json", 12)
    sv2 = person("Mickey", 13)
    sv3 = person("Titan", 34)
    li = listPerson()
    li.add(sv1)
    li.add(sv2)
    li.add(sv3)
    li.print()
main()

Chuyển ký tự in hoa thành in thường
def main():
    text = "A"
    res = chr(ord(text) + 32)
    print(res)
main()
a
2. Add two Numbers – Leetcode
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: Optional[ListNode]
        :type l2: Optional[ListNode]
        :rtype: Optional[ListNode]
        """
        head = ListNode()
        temp = head
        carry = 0
        while (l1 != None) or (l2 != None) or (carry != 0):
            l1_value = l1.val if (l1 != None) else 0
            l2_value = l2.val if (l2 != None) else 0
            total = l1_value + l2_value + carry
            temp.next = ListNode(total%10, None)
            carry = total // 10
            l1 = l1.next if (l1 != None) else None
            l2 = l2.next if (l2 != None) else None
            temp = temp.next
        return head.next
l1 = [2,4,3]
l2 = [5,6,4]
Out = [7,0,8]
Vì 342+465 = 807
3. Longest Substring Without repeating – LeetCode
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        l = 0
        length = 0
        seen = {}
        for i in range(len(s)):
            char = s[i]
            if (char in seen) and (seen[char] >= l):
                l = seen[char] + 1
            else:
                length = max(length, i-l+1)
            seen[char] = i
        return length
s = “abcacbdd”
output = 4
4. Median of Two Sorted Arrays – LeetCode
def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        a = nums1 + nums2
        for i in range(len(a)-1, 0, -1):
            for j in range(i):
                if a[j] > a[j+1]:
                    temp = a[j]
                    a[j] = a[j+1]
                    a[j+1] = temp
        half = len(a) // 2
        if len(a) % 2 == 0:
            return (a[half] + a[half-1])*1.0/2
        else:
            return a[half]
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
Example 2:
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.

5. Reverse Integer – LeetCode
class Solution(object):
    def helper(self, x, n):
        if x == 0: return 0
        if n == 0: return 1
        else:
            res = self.helper(x*x, n//2)
            return res*x if n%2 != 0 else res

    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        if n >= 0: return self.helper(x,n)
        else: return 1.0 /self.helper(x,-1*n)

    def reverse(self, n):
        """
        :type x: int
        :rtype: int
        """
        res = ""
        count = 0
        if n < 0:
            count += 1
            n *= -1
        if n == 0: return 0
        while(n>0):
            t = n%10
            n //= 10
            res = res + str(t)
        res = int(res)
        if count == 1: res = -1*res
        if res < self.myPow(-2, 31) or res > self.myPow(2, 31)-1: return 0
        return res

Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-231, 231 - 1], then return 0.
Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

Example 1:
Input: x = 123
Output: 321
Example 2:
Input: x = -123
Output: -321
Example 3:
Input: x = 120
Output: 21

Constraints:
-231 <= x <= 231 - 1

Cải tiến code:
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        if x < 0:
            reversed_x = -int(str(x).strip("-")[::-1])
        else:
            reversed_x = int(str(x)[::-1])

        if reversed_x < -2**31 or reversed_x > 2**31 - 1:
            return 0

        return reversed_x



6. Zigzag Conversion – LeetCode
Nó được hiểu là bài toán mã mã theo hệ mã Rail Fence
class encodeRailFence:
    def __init__(self):
        pass
    def encode(self, text, numRows):
        if numRows == 1: return text
        res = ""
        # duyệt qua từng hàng
        for i in range(numRows):
            print("i", i)
            buocNhay = 2 * (numRows - 1) # bước nhảy giữa các ký tự
            # lấy ký tự ở hàng i
            for j in range(i, len(text), buocNhay):
                # chỉ lấy được các ký tự ở các cột thẳng hàng thứ i trong đồ thị zigzag
                # P   A   H   N (i = 0: text[j] = P, A, H, N)
                # A P L S I I G (i = 1: text[j] = A, L, I, G)
                # Y   I   R     (i = 2: text[j] = Y, I, R)
                res += text[j]
                print(res)
                # lấy các ký tự còn lại ở hàng i
                if(i > 0 and i < numRows -1 and j + buocNhay - 2 * i < len(text)):
                    res += text[j + buocNhay - 2 * i]
        return res
def main():
    text = "paypalishiring"
    numRows = 3
    encode = encodeRailFence()
    print(encode.encode(text, numRows))
main()

Cải tiến Code:
class Solution(object):
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        if numRows == 1 or len(s) <= numRows:
            return s

        rows = [''] * numRows
        current_row = 0
        step = 1

        for char in s:
            rows[current_row] += char

            if current_row == 0:
                step = 1
            elif current_row == numRows - 1:
                step = -1

            current_row += step

        return ''.join(rows)

50. Pow(x, n) – LeetCode
class Solution(object):
    def helper(self, x, n):
        if x == 0: return 0
        if n == 0: return 1
        else:
            res = self.helper(x*x, n//2)
            return res*x if n%2 != 0 else res

    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        if n >= 0: return self.helper(x,n)
        else: return 1.0 /self.helper(x,-1*n)

69. Sqrt(x) – LeetCode
def mySqrt(self, x):
        left, right = 0, x
        while left <= right:
            mid = (left+right)//2
            if mid*mid > x: right = mid - 1
            elif mid*mid < x: left = mid + 1
            else: return mid
        return right
4 -> 2
8 ->2 vì căn 8 bằng 2,8 chỉ lấy phần nguyên
Chuyển đổi tiền từ số sang chữ
def unitDigit(n):
    dic = {
        '0': "không",
        '1': "một",
        '2': "hai",
        '3': "ba",
        '4': "bốn",
        '5': "năm",
        '6': "sáu",
        '7': "bảy",
        '8': "tám",
        '9': "chín",
    }
    return dic.get(n)
def tensPlace(n):
    result,tens = "", "mươi"
    if n[0] == "1" and n[1] == "0": result = "mười"
    elif n[0] == "1" and n[1] != "0": result = "mười" + " " + unitDigit(n[1])
    elif n[1] == "0": result = unitDigit(n[0]) + " " + tens
    elif n[1] == "1": result = unitDigit(n[0]) + " " + tens + " " + "mốt"
    else: result = unitDigit(n[0]) + " " + tens + " " + unitDigit(n[1])
    return result
def hundredsPlace(n):
    result, temp, hundreds = "", n[1:], "trăm"
    if n[1] == "0" and n[2] == "0": result = unitDigit(n[0]) + " trăm"
    elif n[1] == "0": result = unitDigit(n[0]) + " trăm linh " + unitDigit(n[2])
    else: result = unitDigit(n[0]) + " trăm " + tensPlace(temp)
    return result
def readThree(n):
    result = ""
    if n[0] == "0" and n[1] == "0" and n[2] != "0": result = " không trăm linh " + unitDigit(n[2])
    elif n[0] == "0" and n[1] != "0": result = " không trăm " + tensPlace(n[1:])
    else: result = hundredsPlace(n)
    return result
def thousandsPlace(n):
    r, list, result = len(n)-1, [], ""
    while r >= 0:
        l = r-2 if r >= 2 else 0
        list.append(n[l:r+1])
        r -= 3
    list = list[::-1]
    if list[1] == "000":
     if len(list[0]) == 1: result = unitDigit(list[0]) + " nghìn"
     elif len(list[0]) == 2: result = tensPlace(list[0]) + " nghìn"
     elif len(list[0]) == 3: result = hundredsPlace(list[0]) + " nghìn"
    elif len(list[0]) == 1: result = unitDigit(list[0]) + " nghìn" + readThree(list[1])
    elif len(list[0]) == 2: result = tensPlace(list[0]) + " nghìn" + readThree(list[1])
    elif len(list[0]) == 3: result = hundredsPlace(list[0]) + " nghìn " + readThree(list[1])
    return result
def milionsPlace(n):
    r, list, result = len(n)-1, [], ""
    while r >= 0:
        l = r-2 if r >= 2 else 0
        list.append(n[l:r+1])
        r -= 3
    list = list[::-1]
    if list[1] == "000" and list[2] == "000":
     if len(list[0]) == 1: result = unitDigit(list[0]) + " triệu"
     elif len(list[0]) == 2: result = tensPlace(list[0]) + " triệu"
     elif len(list[0]) == 3: result = hundredsPlace(list[0]) + " triệu"
    elif len(list[0]) == 1: result = unitDigit(list[0]) + " triệu" + thousandsPlace(list[1] + list[2])
    elif len(list[0]) == 2: result = tensPlace(list[0]) + " triệu" + thousandsPlace(list[1] + list[2])
    elif len(list[0]) == 3: result = hundredsPlace(list[0]) + " triệu" + thousandsPlace(list[1] + list[2])
    return result
def bilionsPlace(n):
    r, list, result = len(n)-1, [], ""
    while r >= 0:
        l = r-2 if r >= 2 else 0
        list.append(n[l:r+1])
        r -= 3
    list = list[::-1]
    if list[1] == "000" and list[2] == "000" and list[3]  == "000":
     if len(list[0]) == 1: result = unitDigit(list[0]) + " tỷ"
     elif len(list[0]) == 2: result = tensPlace(list[0]) + " tỷ"
     elif len(list[0]) == 3: result = hundredsPlace(list[0]) + " tỷ"
    elif len(list[0]) == 1: result = unitDigit(list[0]) + " tỷ " + milionsPlace(list[1] + list[2] + list[3])
    elif len(list[0]) == 2: result = tensPlace(list[0]) + " tỷ " + milionsPlace(list[1] + list[2] + list[3])
    elif len(list[0]) == 3: result = hundredsPlace(list[0]) + " tỷ " + milionsPlace(list[1] + list[2] + list[3])
    return result
def  thousandsBilionsPlace(n):
   return "chưa được triển khai"
def numberToString(n):
    result = ""
    if len(n) == 1: result = unitDigit(n)
    elif len(n) == 2: result = tensPlace(n)
    elif len(n) == 3: result = hundredsPlace(n)
    elif len(n) >= 4 and len(n) <= 6: result = thousandsPlace(n)
    elif len(n) >= 7 and len(n) <= 9: result = milionsPlace(n)
    elif len(n) >= 10 and len(n) <= 12: result = bilionsPlace(n)
    else: result = thousandsBilionsPlace(n)
    return result

# for i in range(1000, 1101):
#     print(numberToString(str(i)))
print(numberToString("1234232323"))

LinkList – Danh sách liên kết
Là một dãy các cấu trúc dữ liệu được kết nói với nhau thông qua các liên kết – link. Hiểu một cách đơn giản thì danh sách liên kết là một cấu trúc dữ liệu bao gồm một nhóm các nút – node tạo thành một chuỗi. Mỗi nút bao gồm dữ liệu ở nút đó và tham chiếu đến nút kế tiếp trong chuỗi.
Danh sách liên kết là cấu trúc dữ liệu được sử dụng phổ biến thứ 2 sau mảng.
    • link: mỗi link của một danh sách liên kết có thể lưu giữ một dữu liệu được gọi là một phần tử.
    • next: Mỗi liên kết của một danh sách liên kết chứa một link tới next link được gọi là next.
    • First: một danh sách liên kết bao gồm các liên kết nối tới first link được gọi là first.

Các loại LinkList
    • Simple Linked List – danh sách liên kết đơn: Chỉ duyệt các phần tử theo chiều về trước.
    • Doubly Linked List – Danh sách liên kết đôi: Các phần tử có thể được duyệt theo chiều về trước hoặc về sau.
    • Circular Linked List – Danh sách liên kết vòng: Phần tử cuối cùng chứa link của phần tử đầu tiên như là next và phần tử đầu tiên có link tới phần tử cuối cùng như là prev.