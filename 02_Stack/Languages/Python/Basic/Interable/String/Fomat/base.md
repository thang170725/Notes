Fomat()
Định dạng các giá trị đã chỉ định và chèn chúng vào bên trong trình giữ chỗ của chuỗi. Trình giữ chỗ được định nghĩa bằng dấu ngoặc nhọn.
Cú pháp:
    • <variable>.fomat(value1, value2, …)
    • String.fomat(value1, value2, …)
# case 1
txt1 = "My name is {name}, i am from {country}"
txt1 = txt1.format(name = "Thang", country = "Viet Nam")
print(txt1)
# case 2
txt2 = "My name is {name}, i am from {country}".format(name = "Thang", country = "Viet Nam")
print(txt2)
# case 3
txt3 = "My name is {0}, i am from {1}".format("Thang", "Viet Nam")
print(txt3)
# case 4
txt4 = "My name is {}, i am from {}".format("Thang", "Viet Nam")
print(txt4)
My name is Thang, i am from Viet Nam
My name is Thang, i am from Viet Nam
My name is Thang, i am from Viet Nam
My name is Thang, i am from Viet Nam

:>
Thiết lập 8 khoảng trắng và căn giá trị phần tử sang phải.
txt = "We have {:>8} chickens."
print(txt.format(49))
We have       49 chickens.
:^
Thiết lập 15 khoảng trắng và căn giá trị phần tử vào giữa.
txt = "He is from {:^15}".format("VietNam")
print(txt)
He is from     VietNam
:=
Thiết lập 15 khoảng trắng và căn các ký dấu sang một bên, số sang một.
txt = "He is from {:=15}".format(-5)
print(txt)
He is from -             5
:+
Để chỉ định một số được biểu diễn là số dương hay âm.
txt = "{:+5}, {:+5}".format(-3, 3)
print(txt)
-   3, +    3
:-
Để luôn chỉ ra nếu số là âm, số dương được hiển thị mà không có dấu nào.
txt = "{:-}, {:-}".format(-3, 3)
print(txt)
-3, 3
:
Để chèn một ký tự nào đó vào chuỗi.
:,
Để thêm dấu phân cách hàng nghìn.
str = "{:,}".format(12300000000)
print(str)
12,300,000,000
:_
Để thêm dấu gạch dưới phân cách hàng nghìn.
txt = "The universe is {:_} years old."
print(txt.format(13800000000))
The universe is 13_800_000_000 years old.
:b
Để chuyển một số sang hệ nhị phân.
str = "{} = {:b}".format(5,5)
print(str)
5 = 101
:d
Để chuyển số từ hệ nhị phân sang hệ thập phân.
str = "{:d}".format(0b101)
print(str)
5
:e
txt = "We have {:e} chickens."
print(txt.format(5))
We have 5.000000e+00 chickens.
:E
txt = "We have {:E} chickens."
print(txt.format(5))
We have 5.000000E+00.
:f
txt = "The price is {:.3f} dollars."
print(txt.format(45))
txt = "The price is {:f} dollars."
print(txt.format(45))
The price is 45.000 dollars.
The price is 45.000000 dollars.

:F
x = float('inf')
txt = "The price is {:F} dollars."
print(txt.format(x))
txt = "The price is {:f} dollars."
print(txt.format(x))
The price is INF dollars.
The price is inf dollars.
:o
txt = "The octal version of {0} is {0:o}"
print(txt.format(10))
The octal version of 10 is 12
:X
txt = "The Hexadecimal version of {0} is {0:X}"
print(txt.format(255))
The Hexadecimal version of 255 is FF
:%
txt = "You scored {:%}"
print(txt.format(0.25))
txt = "You scored {:.0%}"
print(txt.format(0.25))
You scored 25.000000%
You scored 25%
Format_map
Hàm này cho phép chúng ta thực hiện ddinhj dạng chuỗi sử dụng các giá trị tù một bản đồ dữ liệu (mapping). 
Cú pháp:
String.fomat_map(mapping)
    • String là chuỗi mình muốn định dạng.
    • Mapping là đối tượng bản đồ dữ liệu (dictionary-like object) chứa các giá trị cho việc định dạng chuỗi.
person = {'name': 'Alice', 'age': 25}
message = 'My name is {name} and I am {age} years old.'
formatted_message = message.format_map(person)
print(formatted_message)
My name is Alice and I am 25 years old.
encode()
Để mã hóa chuỗi, sử dụng mã hóa được chỉ định. Nếu không chỉ định mã hóa, UTF-8 sẽ được sử dụng.
Cú pháp: <variable>.encode(encoding=encoding, errors=errors)
Parameter
Description
encoding
Optional. A String specifying the encoding to use. Default is UTF-8
errors
Optional. A String specifying the error method. Legal values are:
'backslashreplace'
- uses a backslash instead of the character that could not be encoded
'ignore'
- ignores the characters that cannot be encoded
'namereplace'
- replaces the character with a text explaining the character
'strict'
- Default, raises an error on failure
'replace'
- replaces the character with a questionmark
'xmlcharrefreplace'
- replaces the character with an xml character