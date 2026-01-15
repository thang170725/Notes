 [\*args](#args)
- [\*args](#args)
- [\*\*kwargs](#kwargs)
- [Keyword Arguments](#keyword-arguments)
- [Keyword-Only Arguments](#keyword-only-arguments)

---

# *args
```bash
- Nếu bạn không biết có bao nhiêu đối số sễ được truyền vào hàm.
- Theo cách này, hàm sẽ nhận được một bộ đối số và có thể truy cập theo list.
```
**Ex**
```python
def my_function(*kids):
  print("The youngest child is " + kids[2])
my_function("Emil", "Tobias", "Linus") # The youngest child is Linus
```

# **kwargs
```bash
- Nếu bạn không biết có bao nhiêu đối số từ khóa sẽ được truyền vào hàm 
- Theo cách này, hàm sẽ nhận được một từ điển đối số và có thể truy cập được vào các mục tương ứng.
```
**Ex**
```python
def my_function(**kid):
  print("His last name is " + kid["lname"])
my_function(fname = "Tobias", lname = "Refsnes") # His last name is Refsnes
```

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