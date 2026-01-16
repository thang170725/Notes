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