⭐ 1. __slots__ – tối ưu bộ nhớ (cặp bài trùng với dict)
class User:
    __slots__ = ("name", "age")

    def __init__(self, name, age):
        self.name = name
        self.age = age


📌 Điều đặc biệt:

❌ Không có __dict__

❌ Không thêm attribute linh tinh

✅ Tiết kiệm RAM (quan trọng khi tạo hàng triệu object)

u = User("An", 20)
u.email = "x@gmail.com"   # ❌ AttributeError


👉 Rất hay cho:

data object

DTO

model
khi nào dùng slots, lấy ví dụ dễ hiểu để thấy sự khác biệt cho tôi

Câu này rất đúng chỗ đau của người viết class nhiều 👍
__slots__ không phải lúc nào cũng dùng, nhưng dùng đúng thì rất “đáng tiền”.

Mình sẽ giải thích theo thứ tự:
1️⃣ __slots__ là gì (hiểu trong 30 giây)
2️⃣ Ví dụ SO SÁNH TRỰC TIẾP (thấy khác ngay)
3️⃣ Khi nào NÊN dùng / KHÔNG nên dùng
4️⃣ Checklist quyết định nhanh

1️⃣ __slots__ là gì? (cực dễ hiểu)

👉 Bình thường:

Mỗi object có __dict__

__dict__ lưu attribute dạng key-value

→ linh hoạt nhưng tốn RAM

👉 __slots__ nói với Python:

“Object này chỉ được phép có những attribute này thôi, đừng tạo __dict__ nữa”

2️⃣ Ví dụ so sánh trực tiếp (RẤT QUAN TRỌNG)
❌ Không dùng __slots__
class User:
    def __init__(self, name, age):
        self.name = name
        self.age = age

u = User("An", 20)
print(u.__dict__)


📌 Output:

{'name': 'An', 'age': 20}


✔️ Có thể làm bậy:

u.email = "a@gmail.com"   # OK
u.xyz = 123               # OK


➡️ Object phình to dần mà bạn không kiểm soát.

✅ Dùng __slots__
class User:
    __slots__ = ("name", "age")

    def __init__(self, name, age):
        self.name = name
        self.age = age

u = User("An", 20)
print(hasattr(u, "__dict__"))


📌 Output:

False


❌ Không thể làm bậy:

u.email = "a@gmail.com"
# AttributeError: 'User' object has no attribute 'email'


💡 Bạn thấy sự khác biệt ngay chưa?

3️⃣ Lợi ích THỰC SỰ của __slots__
⭐ 1. Tiết kiệm RAM (lợi ích lớn nhất)

Mỗi object không có __dict__

Khi có:

10k / 100k / 1M object

→ tiết kiệm RAM rất đáng kể

📌 Dùng cho:

data model

game entity

ML / simulation

cache object

⭐ 2. Chặn bug do gán nhầm attribute
u.ag = 20   # typo


❌ Không dùng slots → bug âm thầm
✅ Dùng slots → crash sớm

⭐ 3. Object “cứng” hơn → dễ bảo trì

👉 Nhìn class là biết object có gì – không có gì

4️⃣ Khi NÀO nên dùng __slots__
✅ NÊN dùng khi:

✔️ Class giống data object
✔️ Số attribute cố định
✔️ Tạo nhiều instance
✔️ Muốn tránh typo / attribute linh tinh

📌 Ví dụ:

User(id, name, age)

Point(x, y)

Order(id, price, status)

DTO / Value Object

Ví dụ rất chuẩn
class Point:
    __slots__ = ("x", "y")

    def __init__(self, x, y):
        self.x = x
        self.y = y

5️⃣ Khi KHÔNG nên dùng __slots__
❌ KHÔNG dùng khi:

❌ Cần gán attribute động
❌ Object mang tính “mở”
❌ Dùng nhiều metaprogramming
❌ Framework / plugin system
❌ Cần monkey-patch

📌 Ví dụ không nên:

class RequestContext:
    pass

ctx = RequestContext()
ctx.user = user
ctx.request_id = "abc"
ctx.locale = "vi"


➡️ Class này bắt buộc phải có __dict__

6️⃣ __slots__ + @property (combo rất hay)
class User:
    __slots__ = ("_salary",)

    def __init__(self, salary):
        self.salary = salary

    @property
    def salary(self):
        return self._salary

    @salary.setter
    def salary(self, value):
        if value < 0:
            raise ValueError
        self._salary = value


✔️ Vừa:

tiết kiệm RAM

vừa encapsulation

vừa an toàn

7️⃣ __slots__ và kế thừa (rất hay bị sai)
class Base:
    __slots__ = ("a",)

class Child(Base):
    __slots__ = ("b",)


❗ Nếu quên __slots__ ở subclass → __dict__ quay lại

8️⃣ Checklist quyết định nhanh (CHỐT)

Trước khi dùng __slots__, tự hỏi:

❓ Object này có cần thêm attribute về sau không?

Trả lời	Dùng __slots__?
Không	✅ Có
Có	❌ Không
9️⃣ Một câu chốt rất đáng nhớ

🔥 __slots__ biến object từ “túi nilon” thành “khuôn cứng”
Linh hoạt ↓ – An toàn & hiệu năng ↑

Nếu bạn muốn, mình có thể:

Benchmark RAM thật sự (so sánh slots vs dict)

So sánh __slots__ vs dataclass(slots=True)

Cho guideline dùng __slots__ trong project lớn

Refactor 1 class bạn đang dùng sang slots

👉 Bạn thường tạo class kiểu data model, service, hay framework?