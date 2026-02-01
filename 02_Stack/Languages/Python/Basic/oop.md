- [class](#class)
  - [__dict__](#dict)
- [__init__() \& __str__() \& __len__()](#init--str--len)
  - [__mro__](#mro)
  - [__call__()](#call)
  - [__getitem__()](#getitem)
  - [__add__() \& __sub__() \& __mul__() \& __truediv__()](#add--sub--mul--truediv)
  - [__iadd()__ \& __isub__() \& __imul__() \& __itruediv__() __iffloordiv__ \& __imod__() \& __ipow__()](#iadd--isub--imul--itruediv-iffloordiv--imod--ipow)
  - [__lt__() \& __gt__() \& __eq__() \& __ne__() \& __le__() \& __ge__()](#lt--gt--eq--ne--le--ge)
  - [__neg__()](#neg)
  - [setattr() \& __setattr__()](#setattr--setattr)
  - [Del](#del)
  - [__pos__() \& __abs__() \& __invert__()](#pos--abs--invert)
  - [__floordiv__() \& __mod__() \&  __divmod__()](#floordiv--mod---divmod)
  - [a.__lshift__(b)](#alshiftb)
  - [__radd__() \& __rsub__() __rmul__()](#radd--rsub-rmul)
  - [\_rtruediv() \& rfloordiv \& rmod() \& __rpow__()](#_rtruediv--rfloordiv--rmod--rpow)
  - [__bool__](#bool)
  - [__setitem__() \& delitem\_\_() \& __contains__()](#setitem--delitem__--contains)
  - [__iter__() \& __next__()](#iter--next)
  - [__enter__() \& exit()](#enter--exit)
  - [__get__() \& __set__() \& __delete()__](#get--set--delete)
  - [__set\_name__()](#set_name)
  - [@property](#property)
  - [@classmethod](#classmethod)
    - [Quản lý kết nối Database (Mô phỏng)](#quản-lý-kết-nối-database-mô-phỏng)
  - [Inheritance (Kế thừa)](#inheritance-kế-thừa)
    - [Lớp truu tuong nap rut tien](#lớp-truu-tuong-nap-rut-tien)
  - [duck typing (Python-style)](#duck-typing-python-style)
- [callable()](#callable)
---
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
# class
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
## __dict__
```bash
- Là nơi Python lưu tất cả thuộc tính của object hoặc class
- Nó là dictionary thật sự, không phải khái niệm trừu tượng.
```
**Ex1: lấy các thuộc tính trong class**
```python
class User:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def calc_age(self):
        pass
    
    def calc_salary(self):
        pass
u = User("An", 20)
print(u.__dict__) # {'name': 'An', 'age': 20}
print(User.__dict__) # {'__module__': '__main__', '__init__': <function User.__init__ at 0x7a9eec38ac20>, 'calc_age': <function User.calc_age at 0x7a9eec38bac0>, 'calc_salary': <function User.calc_salary at 0x7a9eec38bd00>, '__dict__': <attribute '__dict__' of 'User' objects>, '__weakref__': <attribute '__weakref__' of 'User' objects>, '__doc__': None}
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
# __init__() & __str__() & __len__()	
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
## __mro__
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
## __iadd()__ & __isub__() & __imul__() & __itruediv__() __iffloordiv__ & __imod__() & __ipow__()
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
```
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
## __neg__()
```bash
- Để định nghĩa toán tử dấu trừ.
```
**Ex**
```python
class Point:
    def __init__(self, x):
        self.x = x

    def __neg__(self):
        return Point(-self.x)

p = Point(10)
q = -p

print(p.x)  # 10
print(q.x)  # -10
```
## setattr() & __setattr__() 
```bash
- Để gán (hoặc tạo mới) thuộc tính cho object bằng tên động (string). Nó rất hay dùng khi viết code linh hoạt, meta-programming, hoặc xử lý dữ liệu động.
- khi gọi setattr(obj, "x", 5) python thực chất gọi obj __setattr__("x", 5)
```
**Syn**
```bash
setattr(object, name, value)

- object    : đối tượng cần gán thuộc tính
- name	    : tên thuộc tính (chuỗi)
- value	    : giá trị muốn gán

- Tương đương với: object.name = value. nhưng name có thể là biến, không cần cố định.
```
**Ex1: setattr**
```python
class Person:
    pass

p = Person()

setattr(p, "name", "An")
setattr(p, "age", 20)

print(p.name)  # An
print(p.age)   # 20

# Nếu thuộc tính chưa tồn tại → Python tạo mới
# Nếu đã tồn tại → Python ghi đè
```
**Ex2: setattr & __setattr__**
```python
class A:
    def __setattr__(self, name, value):
        print(f"Gán {name} = {value}")
        super().__setattr__(name, value)

a = A()
setattr(a, "x", 10)

Gán x = 10
```
## Del
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
## __pos__() & __abs__() & __invert__()
## __floordiv__() & __mod__() &  __divmod__()
```bash
- __floordiv    : //
- __mod__       : %
```
**Ex**
```python
class Candies:
    def __init__(self, total):
        self.total = total

    def __floordiv__(self, people):
        # mỗi người được bao nhiêu viên
        return self.total // people

    def __mod__(self, people):
        # còn dư bao nhiêu viên
        return self.total % people

    def __divmod__(self, people):
        # trả về (mỗi người, dư)
        return (self.total // people, self.total % people)

c = Candies(17)

print(c // 5)          # 3
print(c % 5)           # 2
print(divmod(c, 5))    # (3, 2)
```
## a.__lshift__(b)
Dịch bit sang phải a >> b a.__rshift__(b)
Phép AND a & b a.__and__(b)
Phép OR a | b a.__or__(b)
Phép XOR a ^ b a.__xor__(b)
Phép NOT ~a a.__invert__()
## __radd__() & __rsub__() __rmul__()
## _rtruediv() & rfloordiv & rmod() & __rpow__()
## __bool__
## __setitem__() & delitem__() & __contains__()
## __iter__() & __next__()
```bash
- __iter__  : chuẩn bị để lặp, trả về iterator
- __next__  : lấy phần tử kế tiếp
```
**Ex: Đếm số từ 1 đến 3**
```python
 class Counter:
    def __init__(self, max_value):
        self.max_value = max_value
        self.current = 0

    def __iter__(self):
        return self   # chính object này là iterator

    def __next__(self):
        if self.current >= self.max_value:
            raise StopIteration
        self.current += 1
        return self.current

c = Counter(3)

for x in c:
    print(x)

# 1
# 2
# 3
```
## __enter__() & exit()
__getattr__()     # khi attribute không tồn tại
__getattribute__()# mọi lần truy cập attribute    
__delattr__()
__int__()     # int(obj)
__float__()   # float(obj)
__complex__() # complex(obj)
__index__()   # dùng trong slicing
__new__()     # tạo instance (trước __init__)
__del__()     # destructor
__hash__()    # dùng làm key dict / set
__hash__()    # dùng làm key dict / set
__class__
__slots__
__sizeof__()
__dir__()
## __get__() & __set__() & __delete()__
**Syn**
```bash
class Descriptor:
    def __get__(self, instance, owner):
        ...

    def __set__(self, instance, value):
        ...

    def __delete__(self, instance):
        ...

- instance	: object đang truy cập (vd: obj)
- owner	    : class chứa descriptor
- value	    : giá trị gán
```
**Ex: giới hạn tuổi >= 0**
```python
class PositiveInt:
    def __get__(self, instance, owner):
        return instance.__dict__.get("_age", 0)

    def __set__(self, instance, value):
        if value < 0:
            raise ValueError("Age phải >= 0")
        instance.__dict__["_age"] = value

    def __delete__(self, instance):
        del instance.__dict__["_age"]

class Person:
    age = PositiveInt()

p = Person()

p.age = 20
print(p.age)     # 20

p.age = -5       # ValueError

```
## __set_name__()
```bash 
- Được Python gọi khi class được tạo
- Dùng để descriptor biết tên attribute nó gắn vào
```
Ví dụ:
class PositiveInt:
    def __set_name__(self, owner, name):
        self.private_name = "_" + name

    def __get__(self, instance, owner):
        return instance.__dict__.get(self.private_name, 0)

    def __set__(self, instance, value):
        if value < 0:
            raise ValueError("Phải >= 0")
        instance.__dict__[self.private_name] = value

Dùng:
class Person:
    age = PositiveInt()
    score = PositiveInt()


📌 Lúc này:

age → lưu vào _age

score → lưu vào _score

Không cần hard-code _age nữa 👍
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
- Kế thừa chỉ đáng dùng khi có CẢ 3 điều kiện:
    + Có hành vi chung thật sự
    + Không chỉ giống tên biến. Mà là logic giống nhau
    + Quan hệ is-a không bị gượng
- Student is a Person → OK. Nhưng Student is a Employee? ❌
- Class cha ổn định lâu dài. Ít thay đổi. Nếu cha đổi → con vỡ dây chuyền
-> Thiếu 1 trong 3 → đừng kế thừa
```
**Vì sao kế thừa bị ghét trong code thật?**
```bash
1. Coupling chặt
    + Class con phụ thuộc class cha
    + Cha đổi → con có thể hỏng
2. Hierarchy sâu → khó debug
Person
 └── Employee
      └── Teacher
           └── HeadTeacher
-> Debug xong muốn nghỉ việc
```
### Lớp truu tuong nap rut tien
```bash
from abc import ABC, abstractmethod

class Account:
    @abstractmethod
    def deposit(self):
        ... 
        
    @abstractmethod
    def withdraw(self):
        ...
        
    @abstractmethod
    def get_balance(self):
        ...
    
class SavingsAccount(Account):
    def __init__(self, balance, price):
        self.balance = balance
        self.price = price
    
    def withdraw(self):
        super().withdraw()
        if self.balance < self.price:
            raise ValueError("Khong rut duoc")
        self.balance -= self.price
        print(f'da rut {self.price}')
    
class CheckingAccount(Account):
    def __init__(self, balance, limit):
        self.balance = balance
        self.limit = limit
    
    def withdraw(self):
        super().withdraw()
        if self.balance < self.limit:
            raise ValueError(f'chi duoc no han muc la {self.limit}')
        print('han muc van du')

s = SavingsAccount(10_000, 20_000)
s.withdraw()
c = CheckingAccount(s.balance, -10_000)
```
## duck typing (Python-style)
[Link](../Libraries/Datascience-mathnumeric/Typing/protocol.md)
**Ex1: Protocol (Python hiện đại)**
**Ưu điểm**
```bash
- Không cần kế thừa
- Rất sạch
- Rất dùng nhiều trong code lớn
```
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