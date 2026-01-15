```bash
- Các mục set không được sắp xếp theo thứ tự, không thể thay đổi và không cho phép các giá trị trùng lặp.
- Sử dụng set để:
    + Loại bỏ các phần tử trùng lặp.
    + Kiểm tra sự tồn tại của một phần tử.
    + Thực hiện các phép toán tập hợp.
    + Lưu trữ dữ liệu không có thứ tự và duy nhất.
    + Tối ưu hóa hiệu năng.
```
**Syn**
```bash
<variable> = {value1, value2, …}
<variable> = set((value1, value2, …))
```
**Ex**
```python
thisset = {"apple", "banana", "cherry", True, 1, 2}
print(thisset)

# {True, 2, 'apple', 'banana', 'cherry'}
# 1 không xuất hiện vì nó coi 1 và true là phần tử trùng lặp.
```
Lấy từng phần tử trong set
mySet = {1,2,3,4,5,6,7}
for s in mySet:
    print(s)
# với trường hợp này nó sẽ in ra đúng thứ tự
1
2
3
4
5
6
7
in
Để tìm kiếm một phần tử có trong một set hay không.
mySet = {1,2,3,4,5,6,7,8,9}
print(11 in mySet)
False
add()
Để thêm một phần tử vào trong một set. 
Cú pháp: <variable>.add(value)
thisset = {"apple", "banana", "cherry"}
thisset.add("orange")
print(thisset)
{'apple', 'cherry', 'banana', 'orange'}
update()
Để thêm các mục từ tập hợp khác vào tập hợp hiện tại.
Cú pháp:  <variable>.update(value)
mySet= {"apple"}
orther = {"banana"}
mySet.update(orther)
print(mySet)
{'apple', 'banana'}
union()
Trả về một set mới với các giá trị phần tử là 2 set cũ.
Cú pháp:
    • <variable>.union(<variable1>, <variable2>, …)
    • <variable1> | <variable2> | …
mySet= {"apple", "banana", }
orther = {"orange", "Lemon", "Passion"}
Set = mySet.union(orther)
print(Set)
{'banana', 'apple', 'orange', 'Passion', 'Lemon'}
mySet= {"apple", "banana", }
orther = {"orange", "Lemon", "Passion"}
Set = mySet | orther
print(Set)
{'Passion', 'orange', 'Lemon', 'banana', 'apple'}
remove()
Để xóa một phần tử ra khỏi set. Nếu không tìm thấy phần tử cần xóa từ ném ra lỗi.
Cú pháp: <variable>.remove(value)
mySet= {"apple", "banana"}
mySet.remove("banana")
print(mySet)
{'apple'}
discard()
Để xóa một phần tử ra khỏi set. Nếu không tìm thấy phần tử cần xóa thì bỏ qua lệnh này.
Cú pháp: <variable>.discard(value)
mySet= {"apple", "banana"}
mySet.discard("banana")
print(mySet)
{'apple'}
pop()
Bạn cũng có thể sử dụng phương thức pop để xóa một mục, nhưng phương thức này sẽ xóa một mục ngẫu nhiên, do đó bạn không thể chắc chắn mục nào sẽ bị xóa.
Cú pháp: <variable>.pop()
mySet= {"apple", "banana", "orange", "Lemon", "Passion"}
x = mySet.pop()
print(x)
print(mySet)
orange
{'apple', 'banana', 'Lemon', 'Passion'}
clear()
Để xóa toàn bộ set.
Cú pháp: <variable>.clear()
mySet= {"apple", "banana", "orange", "Lemon", "Passion"}
mySet.clear()
print(mySet)
set()
del
Để xóa toàn bộ set. Del sẽ xóa cả giá trị set và biến set.
Cú pháp: del <variable>
mySet= {"apple", "banana", "orange", "Lemon", "Passion"}
del mySet
print(mySet)

File "D:\workspace\Python_box\TestPy.py", line 3, in <module>
    print(mySet)
          ^^^^^
NameError: name 'mySet' is not defined
intersection()
Trả về một set mới chỉ chứa các phần tử có trong cả 2 set cũ.
Cú pháp: <variable1>.intersection(<variable2>)
mySet= {"apple", "banana", "orange", "Lemon"}
orther = {"orange", "Lemon", "Passion"}
Set = mySet.intersection(orther)
print(Set)
{'Lemon', 'orange'}
mySet= {"apple", "banana", "orange", "Lemon"}
orther = {"orange", "Lemon", "Passion"}
Set = mySet & orther
print(Set)
{'Lemon', 'orange'}
intersection_update()
Chỉ giữ lại các phần tử trùng lặp, nhưng nó sẽ thay đổi tập hợp gốc thay vì trả về tập hợp mới.
Cú pháp: <variable1>.intersection_update(<variable2>)
mySet= {"apple", "banana", "orange", "Lemon"}
orther = {"orange", "Lemon", "Passion"}
mySet.intersection_update(orther)
print(mySet)
{'orange', 'Lemon'}
