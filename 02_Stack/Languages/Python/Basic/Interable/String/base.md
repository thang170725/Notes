```bash
- Nơi chứa cách hàm, phương thức để xử lý chuỗi.
```

expandtabs()
Đặt kích thước tab theo số khoảng trắng được chỉ định.
Cú pháp: <variable>.expandtabs(tabsize)
txt = "H\te\tl\tl\to"
x = txt.expandtabs(4)
print(x)
H    e    l    l  o
Khoảng cách 1 tab lúc này được đặt bằng 4 dấu cách
isalnum()
Trả về True nếu trong chuỗi chỉ có các chữ cái [a-z] và số [0-9].
Cú pháp: <variable>.isalnum()
txt = "Company12"
x = txt.isalnum()
print(x)
True
isalpha()
Trả về True nếu chuỗi có ít nhất 1 ký tự và tất cả ký tự là chữ cái [a-z]. Nếu không phương thức sẽ trả về false.
Cú pháp: <variable>.isalpha()
a = "thang1"
print(a.isalpha())
False
isascii()
Trả về True nếu tất cả các ký tự đều thuộc trong bảng mã ASCII.
Cú pháp: <variable>.isascii()
isdecimal()
Trả về True nếu tất cả các ký tự trong chuỗi đều là số.
Cú pháp: <variable>.isdecimal()

isnumeric()
    • Trả về True nếu tất cả các ký tự đều là số, nếu không thì trả về false.
    • Các số mũ, như 2 và ¾ cũng được coi là các giá số.
    • -1 và 1.5 không được được coi là các giá trị số, vì tất cả các ký tự trong chuỗi phải là số còn – và . thì không.
Cú pháp: <variable>.isnumeric()
isspace()
Trả về true nếu tất cả ký tự trong chuỗi đều là khoảng trắng.
Cú pháp: <variable>.isspace()
isprintable()
Trả về Tue nếu tất cả các ký tự trong chuỗi đều có thể in được.
Cú pháp: <variable>.isprintable()
casefold()
Tương tự như phương thức lower(), nhưng phương thức casefold() mạnh hơn, tích cực hơn, nghĩa là nó sẽ chuyển đổi nhiều ký tự thành chữ thường hơn và sẽ tìm thấy nhiều kết quả khớp hơn khi so sánh hai chuỗi và cả hai đều được chuyển đổi được bằng phương thức casefold().
Cú pháp: <variable>.casefold
txt = "Hello, And Welcome To My World!"
x = txt.casefold()
print(x)
hello, and welcome to my world!


```


```

capitalize()
Viết hoa kí tự đầu tiên trong chuỗi, tất cả kí tự khác viết thường.
Cú pháp: <variable>.capitalize()
a = "welcome to python"
print(a.capitalize())
Welcome to python
swapcase()
Kí tự viết hoa thì viết thường, kí tự viết thường thì viết hoa.
Cú pháp: <variable>.swapcase()
a = "welcome to python"
print(a.swapcase())
WElCoME tO pYTHON
partition()
Để tìm kiếm một chuỗi đã chỉ định và chia chuỗi thành một bộ gồm 3 phần tử.
    • Phần đầu tiên chứa phần trước chuỗi đã chỉ định.
    • Phần tử thứ hai chứa chuỗi chỉ định.
    • Phần tử thứ ba chứa phần sau chuỗi đã chỉ định.
Cú pháp: <variable>.partition(value)
txt = "I could eat bananas all day"
x = txt.partition("bananas")
print(x)
('I could eat ', 'bananas', ' all day')
rpartition()
Để tìm kiếm lần xuất hiện cuối cùng của một chuỗi đã chỉ định và chia chuỗi thành một bộ gồm ba phần tử.
    • Phần đầu tiên chứa phần trước chuỗi đã chỉ định.
    • Phần tử thứ hai chứa chuỗi chỉ định.
    • Phần tử thứ ba chứa phần sau chuỗi đã chỉ định.
Cú pháp: <variable>.rpatition(value)
txt = "I could eat bananas all day, bananas are my favorite fruit"
x = txt.rpartition("bananas")
print(x)
('I could eat bananas all day, ', 'bananas', ' are my favorite fruit')
.rjust() & .ljust()
căn phải, trái chuỗi, sử dụng một ký tự được chỉ định (mặc định là khoảng trắng) làm ký tự điền.
Cú pháp: 
<variable>.rjust(length, character)
<variable>.ljust(length, character)
txt = "banana"
x = txt.rjust(20, "O")
print(x) # OOOOOOOOOOOOOObanana
txt = "banana"
x = txt.ljust(20, "O")
print(x) # bananaOOOOOOOOOOOOOO
center()
Phương thức này sẽ căn giữa chuỗi, sử dụng một ký tự được chỉ định (mặc định là khoảng trắng) làm ký tự điền.
Cú pháp: <variable>.center(length, character)
txt = "banana"
x = txt.center(20, "O")
print(x)
OOOOOOObananaOOOOOOO


translate()
Trả về một chuỗi trong chuỗi trong đó một số ký tự được chỉ định được thay thế bằng ký tự được mô tả trong từ điển hoặc trong bảng ánh ánh xạ. Nếu sử dụng từ điển, bạn phải sử dụng mã ASCII thayy vì ký tự.
Cú pháp: string.translate(table)
#use a dictionary with ascii codes to replace 83 (S) with 80 (P):
mydict = {83:  80}
txt = "Hello Sam!"
print(txt.translate(mydict))
Hello Pam!
makestrans()
Trả về một bảng ánh xạ có thể được sử dụng với phương thức translate() để thay thế các ký tự đã chỉ định.
Cú pháp: str.maketrans(x, y, z)
    • x: Bắt buộc. Nếu chỉ có một tham số được chỉ định, thì đây phải là một từ điển mô tả cách thực hiện thay thế. Nếu có hai hoặc nhiều tham số được chỉ định, thì tham số này phải là một chuỗi chỉ định các ký tự bạn muốn thay thế.
    • y: Tùy chọn. Một chuỗi có cùng độ dài với tham số x. Mỗi ký tự trong tham số đầu tiên sẽ được thay thế bằng ký tự tương ứng trong chuỗi này.
    • z: Tùy chọn. Một chuỗi mô tả các ký tự nào sẽ xóa khỏi chuỗi gốc.
txt = "Hello Sam!"
mytable = str.maketrans("S", "P")
print(txt.translate(mytable))
Hello Pam!

txt = "Hi Sam!"
x = "mSa"
y = "eJo"
mytable = str.maketrans(x, y)
print(txt.translate(mytable))
Hi Joe!

txt = "Good night Sam!"
x = "mSa"
y = "eJo"
z = "odnght"
mytable = str.maketrans(x, y, z)
print(txt.translate(mytable))
G i Joe!
splitlines()
Chia một chuỗi thành một danh sách. Việc chia được thực hiện tại các ngắt dòng.
Cú pháp: <variable>.splitlines(keeplinebreaks)
Keeplinebreaks: Tùy chọn. Chỉ định cem có nên bao gồm ngắt dòng đúng hay sai không. Giá trị mặc định là sai.
txt = "Thank you for the music\nWelcome to the jungle"
x = txt.splitlines()
print(x)
['Thank you for the music', 'Welcome to the jungle']

txt = "Thank you for the music\nWelcome to the jungle"
x = txt.splitlines(True)
print(x)
['Thank you for the music\n', 'Welcome to the jungle']
zfill()
Thêm số 0 vào đầu chuỗi, cho đến khi đạt đến độ dài nhất định. Nếu giá trị của tham số len nhỏ hơn độ dài của chuỗi, thì không được thực hiện điền.
Cú pháp: <variable>.zfill(len)
a = "hello"
b = "welcome to the jungle"
c = "10.000"
print(a.zfill(10))
print(b.zfill(10))
print(c.zfill(10))
00000hello
welcome to the jungle
000010.000
