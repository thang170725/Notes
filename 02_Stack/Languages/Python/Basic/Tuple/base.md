```bash
- Là một kiểu dữ liệu dùng để lưu trữ các đối tượng không thay đổi về sau (giống như hằng số). Nó sử dụng để lưu trữ nhiều mục trong một biến duy nhất. 
```
**Syn**
```bash
<variable> = (value1, value2, …)
<variable> = tuple((value1, value2, …))
```
**Ex**
```python
days = ("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday")
print(days)
print(type(days))

# ('Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday')
# <class 'tuple'>
```


Add Items
Để thêm một phần tử nào đó vào tuple. Cần phải chuyển sang kiểu dữ liệu list rồi mới thêm.
Cú pháp: <variable>.append(value)
myTuple = (1,2,3)
a = list(myTuple)
a.append(4)
myTuple = tuple(a)
print(myTuple)
(1, 2, 3, 4)

myTuple = (1,2,3)
a = (4,)
myTuple += a
print(myTuple)
(1, 2, 3, 4)
Remove Items
Để xóa một phần tử ra khỏi tuple.
Cú pháp: <variable>.remove(value)
myTuple = (1,2,3)
a = list(myTuple)
a.remove(3)
myTuple = tuple(a)
print(myTuple)
(1, 2)


