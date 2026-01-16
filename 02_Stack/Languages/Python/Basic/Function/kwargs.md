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