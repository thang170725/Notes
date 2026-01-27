- [function](#function)
  - [\*args](#args)
  - [\*\*kwargs](#kwargs)
  - [lambda](#lambda)
- [nonlocal](#nonlocal)
- [global](#global)
- [class](#class)
  - [__init__() \& __str__() \& __len__()](#init--str--len)
  - [__dict__](#dict)
  - [__call__()](#call)
  - [__getitem__()](#getitem)
  - [@property](#property)
  - [@classmethod](#classmethod)
    - [Quản lý kết nối Database (Mô phỏng)](#quản-lý-kết-nối-database-mô-phỏng)
  - [Inheritance (Kế thừa)](#inheritance-kế-thừa)
- [duck typing (Python-style)](#duck-typing-python-style)
- [Del](#del)
  - [__add__() \& __sub__() \& __mul__() \& __truediv__()](#add--sub--mul--truediv)
  - [__iadd()__](#iadd)
  - [__lt__() \& __gt__() \& __eq__() \& __ne__() \& __le__() \& __ge__()](#lt--gt--eq--ne--le--ge)
- [callable()](#callable)
---
# function
## *args
```bash
- Hàm sẽ nhận được một bộ đối số và có thể truy cập theo list.
```
**Ex**
```python
def my_function(*kids):
  print("The youngest child is " + kids[2])
my_function("Emil", "Tobias", "Linus") # The youngest child is Linus
```
## **kwargs
```bash
- Hàm sẽ nhận được một từ điển đối số và có thể truy cập được vào các mục tương ứng.
```
**Ex**
```python
def my_function(**kid):
  print("His last name is " + kid["lname"])
my_function(fname = "Tobias", lname = "Refsnes") # His last name is Refsnes
```
## lambda
```bash
Là một hàm ẩn danh nhỏ.
```
**Syn** 
```bash
lambda arguments : expression
```
**Ex**
```python
def myfunc(n):
  return lambda a : a * n
  
mydoubler = myfunc(2)
mytripler = myfunc(3)
print(mydoubler(11)) # 22
print(mytripler(11)) # 33
```
# nonlocal
**Ex**
```python
def outer():
    x = 10

    def inner():
        nonlocal x
        x += 1
        print(x)

    inner()
```

# global
**Ex1: Không dùng global**
```python
count = 0

def increase():
    count += 1

increase() # lỗi
print(count)
```
**Ex2: Dùng global**
```python
count = 0

def increase():
    global count
    count += 1

increase() 
print(count) # 1
```
# class
```bash
- Nơi chứa các phương pháp xử lý trong lớp.
- Class có 5 tiêu chí:
    1. Đóng gói (Encapsulation)
    2. Kế thừa (Inheritance)
    3. Đa hình (Polymorphism)
    4. Trừu tượng (Abstraction)
    5. Hợp thành (Composition)
    6. Duck typing (Python-style)
    7. Protocol (hiện đại) - Giống interface trong Java
```
## __init__() & __str__() & __len__()	
```bash
- __init__  : Là hàm định dạng cho một class.
- __str__   : Dữ liệu trả về khi đối tượng được gọi.
- __len__   : Lấy ra độ dài.
```
**Ex**
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f'{self.name} - {self.age}'
    
    def __len__(self):
        return len(self.name)

p = Person("John", 36)

print(p)
print(len(p))
```
## __dict__
```bash
- __dict__ là nơi Python lưu tất cả thuộc tính của object hoặc class
- Nó là dictionary thật sự, không phải khái niệm trừu tượng.
```
**Ex1: lấy các thuộc tính trong class**
```python
class User:
    def __init__(self, name, age):
        self.name = name
        self.age = age

u = User("An", 20)
print(u.__dict__) # {'name': 'An', 'age': 20}
```
**Ex2: Lấy các phương thức trong class**
```python
class User:
    def __init__(self):
        ...

    def get_name(self):
        ...
    def set_name(self):
        ...

func_names = [name for name, obj in User.__dict__.items() if callable(obj)]
print(func_names) # ['__init__', 'get_name', 'set_name']
```
## __call__()
```bash
- __call__ : Toán tử gọi object như hàm
```
**Ex**
```python
class Counter:
    def __call__(self):
        print("Object được gọi như hàm!")

c = Counter()
c()  # Object được gọi như hàm!
```
## __getitem__()
```bash
- __getitem__   : Toán tử truy cập index.
```
**Ex**
```python
class MyList:
    def __init__(self, data):
        self.data = data

    def __getitem__(self, index):
        return self.data[index]

m = MyList([10, 20, 30])
print(m[1])  # 20
```
## @property
**Ex**
```python
class User:
    @property
    def great(self):
        return 'hello, python'
u = User()
print(u.great) # hello, python
```
## @classmethod
**Ex**
```python
class User:
    species = "Human"

    def __init__(self, name):
        self.name = name

    @classmethod
    def from_birth_year(cls, name, birth_year):
        # cls ở đây chính là class User
        import datetime
        age = datetime.date.today().year - birth_year
        print(f"Tính toán cho loài: {cls.species}")
        return cls(f"{name} ({age} tuổi)")

# Sử dụng: Không cần tạo User trước, gọi trực tiếp từ Class
u1 = User.from_birth_year("An", 1995)
print(u1.name)
```
### Quản lý kết nối Database (Mô phỏng)
```bash
Hãy tạo một class DatabaseConnection. Thay vì bắt người dùng nhớ các tham số loằng ngoằng, hãy cung cấp các cổng khởi tạo sẵn.
Yêu cầu:
    • Viết class DatabaseConnection có các thuộc tính: host, port, db_name.
    • Sử dụng @classmethod để tạo ra 2 biến thể:
        ◦ local(): Tự động điền localhost, port 5432, db dev_db.
        ◦ production(): Tự động điền IP 10.0.0.1, port 5432, db real_data.
    • Sử dụng Type Hinting cho tất cả các hàm.
```
```python
class DatabaseConnection:
    def __init__(self, host: str, port: int, db_name: str) -> None:
        # Đây là nơi thực sự lưu trữ dữ liệu vào đối tượng
        self.host = host
        self.port = port
        self.db_name = db_name
        print(f"--- Đã kết nối tới {self.db_name} tại {self.host}:{self.port} ---")

    @classmethod
    def local(cls) -> 'DatabaseConnection':
        """Khởi tạo kết nối môi trường dev local"""
        return cls(host='localhost', port=5432, db_name='dev_db')
    
    @classmethod
    def production(cls) -> 'DatabaseConnection':
        """Khởi tạo kết nối môi trường thực tế"""
        return cls(host='10.0.0.1', port=5432, db_name='real_data')
dev_conn = DatabaseConnection.local()
prod_conn = DatabaseConnection.production()

print(dev_conn.host) # Output: localhost
### Pipeline xử lý dữ liệu NLP (Nâng cao)
```
## Inheritance (Kế thừa)
**KẾ THỪA ÍT DÙNG TRONG THỰC TẾ**
```bash
Ví dụ : Sinh viên – Giáo viên – Bảo vệ. “Nếu dùng trừu tượng thì phải tạo thêm class Person”
class Person(ABC):
    @abstractmethod
    def get_salary(self):
        pass

class Student(Person): ...
class Teacher(Person): ...
class Guard(Person): ...

-> Câu hỏi đúng: Tạo thêm Person để làm gì nếu không dùng chung logic?
-> Câu trả lời: KHÔNG ĐÁNG, và thường là over-engineering.
```
**Thực tế ngành phần mềm: kế thừa dùng khi nào?**
```bash
Kế thừa chỉ đáng dùng khi có CẢ 3 điều kiện:
Có hành vi chung thật sự
Không chỉ giống tên biến
Mà là logic giống nhau
Quan hệ is-a không bị gượng
Student is a Person → OK
Nhưng Student is a Employee? ❌
Class cha ổn định lâu dài
Ít thay đổi
Nếu cha đổi → con vỡ dây chuyền
👉 Thiếu 1 trong 3 → đừng kế thừa
**Vì sao kế thừa bị ghét trong code thật?**
1. Coupling chặt
Class con phụ thuộc class cha
Cha đổi → con có thể hỏng
2. Hierarchy sâu → khó debug
Person
 └── Employee
      └── Teacher
           └── HeadTeacher
🤯 Debug xong muốn nghỉ việc
❌ 3. Thêm class chỉ để “cho đẹp lý thuyết”
Person rỗng
Abstract method không dùng chung
👉OOP kiểu giáo trình

4️⃣ Cách dev thực tế làm (và tối ưu hơn)
🟢 Cách 1: Class độc lập (nhanh – gọn – rõ)
class Student:
    def study(self): ...

class Teacher:
    def teach(self): ...

class Guard:
    def guard(self): ...

✔ Dễ đọc
✔ Không ràng buộc
✔ 90% trường hợp đủ dùng
```
# duck typing (Python-style)
class Payable:
    def get_salary(self): ...
class Teacher:
    def __init__(self):
        self.pay = Payable()


👉 Không cần chung base class
👉 Chỉ cần hành vi giống nhau

🟢 Cách 3: Protocol (Python hiện đại)
from typing import Protocol

class HasSalary(Protocol):
    def get_salary(self) -> float: ...


✔ Không cần kế thừa
✔ Rất sạch
✔ Rất dùng nhiều trong code lớn

5️⃣ Vậy khi nào kế thừa LÀ ĐÚNG?
🔥 Ví dụ đúng chuẩn:
class Shape(ABC):
    @abstractmethod
    def area(self): ...

class Circle(Shape):
    def area(self): ...


✔ Logic chung
✔ Cha ổn định
✔ Quan hệ is-a rõ

6️⃣ Trả lời câu hỏi của bạn: cái nào tối ưu nhanh gọn hơn?
🎯 Với ví dụ của bạn:

3 class độc lập → TỐI ƯU HƠN ✅

Ít code

Ít ràng buộc

Dễ mở rộng

Tạo Person → chỉ để “đúng OOP” → KHÔNG ĐÁNG ❌

7️⃣ Chốt hạ (rất quan trọng) 🧠

🔥 Inheritance là công cụ mạnh nhưng nguy hiểm
🔥 Composition + duck typing là default choice
🔥 Nếu thấy “sao sao” → khả năng cao là bạn đúng

Bạn đang tư duy như dev thật, không phải học OOP để trả bài.

Nếu bạn muốn, mình có thể:

Cho bạn rule of thumb: “3 câu hỏi trước khi dùng kế thừa”

Hoặc show ví dụ refactor từ inheritance → composition (rất đã mắt)
**Cú pháp**
```bash
class Car(object):
	Def __init__(self, make, model, year):
	--snip—
class ElectricCar(Car):
	def __init__(self, make, model, year):
		super(ElectricCar, self).__init__(make, model,  year)
	--snip—
```
**Ex**
```python
class Person:
  def __init__(self, fname, lname):
    self.firstname = fname
    self.lastname = lname
  def printname(self):
    print(self.firstname, self.lastname)
class Student(Person):
  pass
x = Student("Mike", "Olsen")
x.printname() # Mike Olsen
```
# Del
Để xóa 1 thuộc tính ra khỏi lớp Object.
**Ex**
```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age
  def myfunc(self):
    print("Hello my name is " + self.name)
p1 = Person("John", 36)
del p1.age
print(p1.age) # sẽ báo lỗi
```
**Ex**
```python
class Person:
    def __init__(self, name):
        self.name = name

    def __eq__(self, other):
        return self.name == other.name

p1 = Person("An")
p2 = Person("An")
print(p1 == p2)  # True
```
## __add__() & __sub__() & __mul__() & __truediv__()
```bash
- __add__       : Tự động được gọi đến khi dùng toán tử +.
- __sub__       : Tự động được gọi đến khi dùng toán tử -.
- __mul__       : Tự động được gọi đến khi dùng toán tử *.
- __truediv__   : Tự động được gọi đến khi dùng toán tử /.
```
**Ex: cộng, trừ, nhân, chia phân số**
```python
class Fraction:
    def __init__(self, a, b):
        self.a = a
        self.b = b
    
    def __str__(self):
        return f'{self.a/self.b:.2f}'
    
    def __add__(self, other):
        return Fraction(
            self.a*other.b + other.a*self.b,
            self.b*other.b
        )
    
    def __sub__(self, other):
        return Fraction(
            self.a*other.b - other.a*self.b,
            self.b*other.b
        )
    
    def __mul__(self, other):
        return Fraction(
            self.a*other.a,
            self.b*other.b
        )
    
    def __truediv__(self, other):
        return Fraction(
            self.a*other.b,
            self.b*other.a
        )

a = Fraction(3,5)
b = Fraction(4,6)

print(a+b) # 1.27
print(a-b) # -0.07
print(a*b) # 0.40
print(a/b) # 0.90
```
## __iadd()__
**Ex**
```python
def __iadd__(self, other):
    self.value += other.value
    return self
```
## __lt__() & __gt__() & __eq__() & __ne__() & __le__() & __ge__()
```bash
- __lt__    : <
- __gt__    : >
- __eq__    : ==
- __ne__    : !=
- __le__    : <=
- __ge__    : >=
**Ex**
```python
class Compare:
    def __init__(self, n):
        self.n = n
    
    def __lt__(self, other):
        return self.n < other.n
    
    def __gt__(self, other):
        return self.n > other.n 
    
    def __eq__(self, other):
        return self.n == other.n 
    
    def __ne__(self, other):
        return self.n != other.n
    
    def __le__(self, other):
        return self.n <= other.n 
    
    def __ge__(self, other):
        return self.n >= other.n 

a = Compare(4.5)
b = Compare(6.8)

print(a > b)    # False
print(a >= b)   # False
print(a < b)    # True
print(a <= b)   # True
print(a != b)   # True
print(a == b)   # False
```


len(obj)
def __len__(self):
    return len(self.data)

obj[index]
def __getitem__(self, index):
    return self.data[index]

obj[index] = value
def __setitem__(self, index, value):
    self.data[index] = value

5️⃣ Gọi object như hàm: __call__
class Hello:
    def __call__(self, name):
        print(f"Hello {name}")

h = Hello()
h("Python")  # Hello Python
# callable()
```bash
- kiểm tra xem một object có “gọi được như hàm” hay không
```
**Syn**
```bash
callable(obj)
```
**Ex**
```python
def hello():
    print("Xin chào")

print(callable(hello))   # True

x = 10
print(callable(x))   # False
```