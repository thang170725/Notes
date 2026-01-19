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