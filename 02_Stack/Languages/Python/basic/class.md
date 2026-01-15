- [__init__()](#init)
- [__str__()](#str)
- [Del](#del)
- [Kế thừa](#kế-thừa)
- [@classmethod](#classmethod)
  - [Bài tập](#bài-tập)
    - [Quản lý kết nối Database (Mô phỏng)](#quản-lý-kết-nối-database-mô-phỏng)
    - [Pipeline xử lý dữ liệu NLP (Nâng cao)](#pipeline-xử-lý-dữ-liệu-nlp-nâng-cao)
- [@staticmethod](#staticmethod)


---

# __init__()
Là hàm định dạng cho một class. Nó giống với constructer trong các ngôn ngữ lập trình hướng đối tượng.
**Ex**
```python
class Animal:
    def __init__(self, name, age):
        self.name = name
        self.age = age
b = Animal("Dog", 12)
print(b.name) # Dog
```

# __str__()
Kiểm soát những gì sẽ được trả về khi đối tượng lớp được biểu diễn dưới dạng chuỗi. Nếu hàm __str__() không được thiết lập, biểu diễn chuỗi của đối tượng sẽ được trả về.
**Ex**
**Không dùng str**
```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age
p1 = Person("John", 36)
print(p1) # <__main__.Person object at 0x15039e602100>
```
**Use str**
```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age
  def __str__(self):
    return f"{self.name}({self.age})"
p1 = Person("John", 36)
print(p1) # John(36)
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

# Kế thừa
Là lớp con. Nó sẽ kế thừa lại các thuộc tính của lớp cha.
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

# @classmethod
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
## Bài tập
### Quản lý kết nối Database (Mô phỏng)
Hãy tạo một class DatabaseConnection. Thay vì bắt người dùng nhớ các tham số loằng ngoằng, hãy cung cấp các cổng khởi tạo sẵn.
Yêu cầu:
    • Viết class DatabaseConnection có các thuộc tính: host, port, db_name.
    • Sử dụng @classmethod để tạo ra 2 biến thể:
        ◦ local(): Tự động điền localhost, port 5432, db dev_db.
        ◦ production(): Tự động điền IP 10.0.0.1, port 5432, db real_data.
    • Sử dụng Type Hinting cho tất cả các hàm.
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
Áp dụng trực tiếp vào dự án NLP của bạn. Hãy tạo một class TextProcessor.
Yêu cầu:
    • Class nhận vào một danh sách các transforms (ví dụ: viết thường, xóa dấu, tách từ).
    • Sử dụng @classmethod để tạo các "Gói xử lý" sẵn:
        ◦ vietnamese_basic(): Trả về một Processor có các hàm xóa dấu và viết thường.
        ◦ social_media_style(): Trả về một Processor có thêm hàm xóa icon và xóa link.
    • Thử thách: Viết một hàm __call__ để khi khởi tạo xong, bạn có thể dùng đối tượng đó như một hàm: processor("Chào Bạn!") -> "chao ban".
import re

class TextProcessor:
    def __init__(self, transforms: list) -> None:
        self.transforms = transforms

    def __call__(self, text: str) -> str:
        for func in self.transforms:
            text = func(text)
        return text

    @staticmethod
    def _remove_icons(text: str) -> str:
        return re.sub(r'[^\w\s,]', '', text)

    @classmethod
    def vietnamese_basic(cls) -> "TextProcessor":
        return cls([str.lower, str.strip])

    @classmethod
    def social_media_style(cls) -> "TextProcessor":
        return cls([str.lower, cls._remove_icons, str.strip])

cleaner = TextProcessor.social_media_style()
print(cleaner("Chào bạn!!! 😊")) # Output: chào bạn
Khởi tạo mô hình AI từ nhiều nguồn (Thực tế nhất)
Hãy viết lại Class Model cho dự án Bất động sản của bạn.
Yêu cầu:
    • Tạo class RealEstateModel.
    • Dùng @classmethod để tạo các cách load khác nhau:
    • from_file(path: str): Load model từ file .pkl.
    • from_pretrained(version: str): Tự động chọn file dựa trên version (v1, v2).
    • empty(): Tạo một model trắng chưa train.
import joblib
import torch

class RealEstateModel:
    def __init__(self, model_obj: any, version: str) -> None:
        self.model = model_obj
        self.version = version

    @classmethod
    def from_file(cls, path: str) -> "RealEstateModel":
        """Khởi tạo bằng cách load file .pkl hoặc .pt"""
        # Giả sử load XGBoost từ joblib
        model_data = joblib.load(path)
        return cls(model_obj=model_data, version="loaded_from_file")

    @classmethod
    def from_pretrained(cls, version: str) -> "RealEstateModel":
        """Tự động tìm model theo phiên bản"""
        paths = {
            "v1": "models/xgb_v1.pkl",
            "v2": "models/pytorch_v2.pt"
        }
        target_path = paths.get(version)
        if not target_path:
            raise ValueError("Phiên bản không tồn tại!")
        
        # Logic load thực tế ở đây...
        return cls(model_obj=None, version=version)

    @classmethod
    def empty(cls) -> "RealEstateModel":
        """Tạo model trắng để chuẩn bị train"""
        return cls(model_obj=None, version="raw")

old_model = RealEstateModel.from_pretrained("v1")
new_model = RealEstateModel.from_file("my_model.pkl")

# @staticmethod
Đây là phương thức "độc lập" nhất. Nó không nhận self (đối tượng), cũng không nhận cls (lớp). Nó giống như một hàm bình thường nhưng được "nhốt" vào trong Class để dễ quản lý.
Đặc điểm: Không biết gì về các biến của lớp hay đối tượng.
Ứng dụng: Dùng cho các hàm tiện ích (utility) có logic liên quan đến Class nhưng không cần thay đổi gì trong Class đó.