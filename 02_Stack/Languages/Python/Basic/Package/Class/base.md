```bash
- Nơi chứa các phương pháp xử lý trong lớp.
```

nhưng nói một hồi tôi lại không biết khi nào thì dùng @classmethod, @staticmethod, khi nào chỉ viết phương thức thường, khi nào thì lại dùng @property, v.v lấy ví dụ để cho thấy sự khác biệt

Câu này rất chuẩn “ngưỡng giữa junior → senior Python” 👍
Nhiều người biết cú pháp nhưng không biết khi nào dùng cái nào.
Mình sẽ không nói lý thuyết suông, mà dùng cùng một ví dụ, đổi cách viết để bạn thấy sự khác biệt rõ ràng.

🎯 TƯ DUY CHỐT (đọc kỹ trước)

Khi viết 1 method, hãy tự hỏi CHỈ 1 câu:

❓ Method này đang làm việc với AI?

Object cụ thể → instance method

Class nói chung → @classmethod

Không cần cả hai → @staticmethod

Giống thuộc tính, không phải hành động → @property

🧩 1 ví dụ DUY NHẤT: User

Giả sử bạn có class:

class User:
    TAX = 0.1

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

1️⃣ INSTANCE METHOD – khi dùng phương thức thường
❓ Khi nào?

✔️ Cần dữ liệu của object cụ thể
✔️ Logic gắn với 1 instance

class User:
    def yearly_salary(self):
        return self.salary * 12


👉 Dùng khi:

self có ý nghĩa

Mỗi object có kết quả khác nhau

📌 Gọi:

u = User("An", 1000)
u.yearly_salary()

2️⃣ @CLASSMETHOD – khi làm việc với CLASS
❓ Khi nào?

✔️ Không quan tâm object nào
✔️ Logic liên quan chung cho class
✔️ Thường dùng để tạo object theo cách khác

Ví dụ 1: alternative constructor
class User:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    @classmethod
    def from_string(cls, s):
        name, salary = s.split(",")
        return cls(name, int(salary))


👉 Dùng:

u = User.from_string("An,1000")


📌 ❌ Không nên viết thế này:

def from_string(s):   # mất cls
    ...

Ví dụ 2: thao tác với class variable
class User:
    TAX = 0.1

    @classmethod
    def set_tax(cls, tax):
        cls.TAX = tax

3️⃣ @STATICMETHOD – khi KHÔNG cần class hay object
❓ Khi nào?

✔️ Logic chỉ là hàm tiện ích
✔️ Đặt trong class cho gần ngữ nghĩa

class User:
    @staticmethod
    def is_valid_name(name):
        return isinstance(name, str) and len(name) > 0


📌 Gọi:

User.is_valid_name("An")


👉 So với viết ngoài class:

def is_valid_name(name): ...


✔️ @staticmethod dùng khi:

Hàm liên quan đến User

Nhưng không cần self, cls

4️⃣ @PROPERTY – khi method TRÔNG NHƯ thuộc tính
❓ Khi nào?

✔️ Không phải hành động
✔️ Chỉ trả về giá trị
✔️ Muốn giấu logic phía sau attribute

❌ Viết không đẹp
u.get_yearly_salary()

✅ Viết đúng Python
class User:
    @property
    def yearly_salary(self):
        return self.salary * 12


📌 Dùng:

u.yearly_salary


💡 Cảm giác: như đọc biến, không gọi hàm

5️⃣ @property + setter – validation “xịn”
class User:
    def __init__(self, salary):
        self.salary = salary

    @property
    def salary(self):
        return self._salary

    @salary.setter
    def salary(self, value):
        if value < 0:
            raise ValueError("salary < 0")
        self._salary = value


👉 Từ ngoài nhìn vào:

u.salary = 1000   # nhưng thực chất có logic

🔥 BẢNG QUYẾT ĐỊNH NHANH (CỰC QUAN TRỌNG)
Tình huống	Dùng
Cần dữ liệu object	instance method
Logic chung cho class	@classmethod
Hàm tiện ích	@staticmethod
Giống attribute	@property
Validate khi gán	@property + setter
Tạo object theo cách khác	@classmethod
🚫 NHỮNG SAI LẦM RẤT HAY GẶP

❌ Dùng @staticmethod nhưng lại cần cls
❌ Dùng instance method nhưng không dùng self
❌ Getter/Setter kiểu Java (get_x(), set_x())
❌ Nhét hết logic vào instance method

🧠 MẸO TƯ DUY (đáng nhớ)

🔹 Nếu bỏ self mà code vẫn chạy → đừng dùng instance method
🔹 Nếu bỏ cls mà vẫn đúng → đừng dùng classmethod
🔹 Nếu đọc thấy “giống biến” → dùng property

🏁 CHỐT HẠ

Python không ép, nhưng Python có triết lý
Dùng đúng loại method → code:

dễ đọc

dễ mở rộng

ít bug

“Pythonic”

Nếu bạn muốn, mình có thể:

Refactor 1 class bạn đang dùng cho đúng kiểu Python

So sánh tư duy Python vs Java (getter/setter)

Cho flowchart chọn method type (nhìn phát hiểu)

👉 Bạn đang viết class cho backend / data / game / tool nội bộ?