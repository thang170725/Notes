# Liệt kê chỉ method bạn định nghĩa trong class
```python
class MyClass:
    def a(self): pass
    def b(self): pass
    def _c(self): pass

    @classmethod
    def d(cls): pass

    @staticmethod
    def e(): pass

methods = [
    name for name, value in MyClass.__dict__.items()
    if callable(value)
]

print(methods) # ['a', 'b', '_c', 'd', 'e']
```

# Chỉ lấy public method (hay dùng)
```python
public_methods = [
    name for name, value in MyClass.__dict__.items()
    if callable(value) and not name.startswith("_")
]

print(public_methods) # ['a', 'b', 'd', 'e']
```

4️⃣ Liệt kê method của INSTANCE (object)
obj = MyClass()

methods = [
    name for name in obj.__class__.__dict__
    if callable(getattr(obj, name))
]

print(methods)


👉 Thường dùng khi bạn chỉ có object, không có class.

5️⃣ Dùng inspect (chuyên nghiệp hơn)
🔥 Dùng khi:

Code lớn

Tool / framework

Auto-doc / CLI

import inspect

methods = inspect.getmembers(MyClass, predicate=inspect.isfunction)
print([name for name, _ in methods])


📌 Output:

['a', 'b', '_c']


⚠️ Lưu ý:

inspect.isfunction → chỉ instance method

Không bắt @classmethod, @staticmethod

👉 Bắt TẤT CẢ method (instance + class + static)
methods = inspect.getmembers(MyClass, predicate=callable)


Nhưng sẽ lẫn nhiều thứ → cần filter thêm.

6️⃣ Chỉ method do mình viết (KHÔNG kế thừa)
def own_methods(cls):
    return [
        name for name, value in cls.__dict__.items()
        if callable(value)
    ]

print(own_methods(MyClass))


👉 Cách này chuẩn nhất nếu bạn sợ lẫn method từ base class.

7️⃣ Bonus xịn: liệt kê kèm loại method
def list_methods(cls):
    result = {}

    for name, value in cls.__dict__.items():
        if isinstance(value, staticmethod):
            result[name] = "static method"
        elif isinstance(value, classmethod):
            result[name] = "class method"
        elif callable(value):
            result[name] = "instance method"

    return result

print(list_methods(MyClass))


📌 Output:

{
 'a': 'instance method',
 'b': 'instance method',
 '_c': 'instance method',
 'd': 'class method',
 'e': 'static method'
}


🔥 Cái này rất hữu dụng khi debug hoặc auto-doc.

8️⃣ Dùng cho thực tế: auto help / debug
def help_methods(cls):
    print(f"Methods of {cls.__name__}:")
    for name in sorted(cls.__dict__):
        if callable(cls.__dict__[name]) and not name.startswith("__"):
            print("-", name)

9️⃣ Tóm tắt nhanh (bạn nên nhớ cái nào)
🟢 Muốn nhanh:
MyClass.__dict__

🔥 Muốn chuẩn, sạch:
callable + __dict__

🧠 Làm tool / framework:
inspect

10️⃣ Kết luận (quan trọng)

🔹 __dict__ là cách chính xác nhất để biết class có gì
🔹 dir() chỉ để xem nhanh, không nên dùng khi cần chính xác
🔹 Khi làm class nhiều, viết sẵn helper list_methods() là cực kỳ đáng

Nếu bạn muốn, mình có thể:

Viết decorator auto-register method

Viết metaclass tự động log method

Tạo CLI inspect class giống Django shell

Giải thích Python lookup attribute chi tiết (MRO)

👉 Bạn đang dùng mấy class này cho framework, game, API hay data model?