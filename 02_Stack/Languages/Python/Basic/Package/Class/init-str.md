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