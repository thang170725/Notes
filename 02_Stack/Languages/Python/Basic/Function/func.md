 [\*args](#args)
- [\*args](#args)
- [\*\*kwargs](#kwargs)
- [Keyword Arguments](#keyword-arguments)
- [Keyword-Only Arguments](#keyword-only-arguments)

---





# Keyword Arguments
```bash
Bạn cũng có thể gửi đối số với cú pháp key = value. Theo cách này, thứ tự của các đối số không quan trọng.
```
**Ex1**
```python
def my_function(child3, child2, child1):
  print("The youngest child is " + child3)
my_function(child1 = "Emil", child2 = "Tobias", child3 = "Linus") # The youngest child is Linus
```
**Ex2**
```python
def my_function(country = "Norway"):
  print("I am from " + country)
my_function("Sweden") # I am from Sweden
my_function("India") # I am from India
my_function() # I am from Norway
my_function("Brazil") # I am from Brazil
```

# Keyword-Only Arguments
```bash
Để chỉ rõ ràng một hàm chỉ có thể có đối số từ khóa, hãy thêm *, trước các đối số.
```
**Ex1**
```python
def my_function(*, x):
  print(x)
my_function(x = 3) # 3

def my_function(*, x):
  print(x)
my_function(3) # lỗi
```