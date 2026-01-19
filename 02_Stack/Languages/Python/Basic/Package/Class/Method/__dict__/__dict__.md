```bash
- __dict__ là nơi Python lưu tất cả thuộc tính của object hoặc class
- Nó là dictionary thật sự, không phải khái niệm trừu tượng.
```
**Ex1**
```python
class User:
    def __init__(self, name, age):
        self.name = name
        self.age = age

u = User("An", 20)
print(u.__dict__) # {'name': 'An', 'age': 20}
```
**Ex2**
```python
print(User.__dict__)

# {
#  '__module__': '__main__',
#  '__init__': <function ...>,
#  '__dict__': <attribute ...>,
#  '__doc__': None
# }
```



⭐ 2. __getattr__ – attribute không tồn tại
class Config:
    def __getattr__(self, name):
        return f"<missing {name}>"

c = Config()
print(c.db_host)


📌 Output:

<missing db_host>


👉 Dùng cho:

config

proxy object

fallback logic

⭐ 3. __getattribute__ – intercept MỌI attribute access
class Debug:
    def __getattribute__(self, name):
        print("Access:", name)
        return super().__getattribute__(name)


⚠️ Rất mạnh – dễ gây bug nếu không cẩn thận
👉 Dùng khi làm framework / ORM

⭐ 4. __setattr__ – kiểm soát gán attribute
class User:
    def __setattr__(self, key, value):
        if key == "age" and value < 0:
            raise ValueError("Age < 0")
        self.__dict__[key] = value


👉 Dùng cho:

validation

immutable object

audit

⭐ 5. __delattr__ – chặn xóa attribute
class Safe:
    def __delattr__(self, name):
        raise AttributeError("Cannot delete")

⭐ 6. __repr__ – cực kỳ quan trọng khi debug
class User:
    def __repr__(self):
        return f"User({self.__dict__})"


📌 Debug cực đã, khỏi print từng field.

⭐ 7. __eq__ + __hash__ – object so sánh thông minh
class User:
    def __eq__(self, other):
        return self.__dict__ == other.__dict__

⭐ 8. __class__ – đổi class runtime (ít người dám dùng 😈)
u.__class__ = AdminUser


👉 Meta-programming / state machine

⭐ 9. __init_subclass__ – hook khi subclass được tạo
class Base:
    def __init_subclass__(cls):
        print("New subclass:", cls.__name__)


👉 Framework, plugin system

⭐ 10. __call__ – object hoạt động như function
class Counter:
    def __call__(self):
        print("Called")

4️⃣ Nếu bạn hay tạo class → nên nhớ bộ này
🔥 MUST KNOW

__dict__

__slots__

__repr__

__eq__

__setattr__

🧠 ADVANCED (framework-level)

__getattr__

__getattribute__

__init_subclass__

__call__

5️⃣ Chốt lại

🔹 __dict__ = “linh hồn” của object/class
🔹 Biết __dict__ → bắt đầu hiểu Python thực sự
🔹 Biết thêm __slots__, __getattr__, __setattr__ → viết class rất khác người thường

Nếu bạn muốn, mình có thể:

So sánh __dict__ vs __slots__ bằng benchmark RAM 📊

Cho checklist magic method theo từng use case

Giải thích Python class internals (lookup attribute diễn ra thế nào)

👉 Bạn muốn đào sâu theo hướng nào?