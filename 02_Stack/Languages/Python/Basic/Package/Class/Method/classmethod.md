Trong Python, @classmethod dùng để tạo phương thức của class, không phải của từng object (instance).

Mình giải thích ngắn gọn – dễ hình dung – có ví dụ đời thường nhé 👇

1️⃣ Hiểu đơn giản nhất

👉 @classmethod là hàm “thuộc về class”

Nó không làm việc trực tiếp với object

Nó làm việc với class

Tham số đầu tiên luôn là cls (đại diện cho class)

📌 So sánh nhanh:

Loại	Thuộc về	Tham số đầu
instance method	object	self
@classmethod	class	cls
@staticmethod	không cần class/object	không có
2️⃣ Ví dụ đời thường (dễ hình dung)
🎓 Ví dụ: Lớp học

Class = Lớp 10A

Object = Học sinh trong lớp

Instance method = “Học sinh này học bài”

Class method = “Cả lớp đổi giáo viên chủ nhiệm”

👉 Việc đổi giáo viên không liên quan đến từng học sinh riêng lẻ, mà liên quan cả lớp → dùng @classmethod

3️⃣ Ví dụ code đơn giản
❌ Không dùng classmethod
class Student:
    school = "ABC School"

    def change_school(self, new_school):
        self.school = new_school


⚠️ Sai logic: mỗi học sinh có thể đổi trường riêng → không đúng

✅ Dùng @classmethod
class Student:
    school = "ABC School"

    @classmethod
    def change_school(cls, new_school):
        cls.school = new_school


👉 Gọi như sau:

Student.change_school("XYZ School")
print(Student.school)


📌 Kết quả:

XYZ School


✔️ Cả class thay đổi

4️⃣ cls là gì?

cls = class hiện tại

Tương tự như:

self → object

cls → class

print(cls)
# <class '__main__.Student'>

5️⃣ Khi nào nên dùng @classmethod?
✅ Dùng khi:

✔️ Cần thao tác với biến class
✔️ Tạo hàm khởi tạo thay thế (alternative constructor)
✔️ Logic liên quan đến class, không phải object

6️⃣ Ví dụ cực hay: Alternative constructor
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def from_birth_year(cls, name, birth_year):
        age = 2025 - birth_year
        return cls(name, age)


👉 Dùng:

p = Person.from_birth_year("An", 2000)
print(p.name, p.age)


📌 Dễ hiểu:

Tạo object Person theo cách khác, nhưng vẫn đúng chuẩn class

7️⃣ So sánh nhanh 3 loại method
class Demo:
    def instance_method(self):
        print("object")

    @classmethod
    def class_method(cls):
        print("class")

    @staticmethod
    def static_method():
        print("nothing")

Method	Dùng khi
instance	Cần dữ liệu object
classmethod	Cần dữ liệu class
staticmethod	Hàm phụ trợ
8️⃣ Tóm tắt ngắn gọn (chốt)

🔹 @classmethod dùng cho các hành động liên quan đến class, không phụ thuộc object
🔹 Dùng cls để truy cập biến class
🔹 Hay dùng để tạo constructor thay thế

Nếu bạn muốn, mình có thể:

Vẽ sơ đồ minh họa 🎨

So sánh classmethod vs staticmethod bằng ví dụ thực tế

Giải thích theo kiểu Java / C++ để dễ liên tưởng

👉 Bạn muốn cách nào?
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