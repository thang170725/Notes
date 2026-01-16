# {}
```bash
- Để lưu trữ giá trị chứa key và value. 
- Có thể sử dụng các thuộc tính của chuỗi và của mảng.
```
**Syn**
```bash
dic = {key: value, …} – name[key]
```

# dict
```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
mydict = dict(thisdict)
print(mydict) # {'brand': 'Ford', 'model': 'Mustang', 'year': 1964}
```



.Keys()
Để lấy ra tên các key.
Cú pháp:
<variable>.keys()
n = {
    1: "một",
    2: "hai"
}
for i in n.keys():
    print(i)
1
2
dir = dict(name='John', age=25, city='New York')
print(dir.keys(), type(dir.keys()))
dict_keys(['name', 'age', 'city']) <class 'dict_keys'>
.values()
Trả về danh sách các giá trị của dictionary.
Cú pháp:
dir = dict(name='John', age=25, city='New York')
print(dir.values())
dict_values(['John', 25, 'New York'])
.items()
Dùng để lấy ra các cặp key, value. Thường dùng trong vòng lặp để lặp qua các key, value. Phương thức này trả về từng mục trong từ điển dưới dạng các bộ trong danh sách.
Cú pháp: 
<variable>.items()
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
x = thisdict.items()
print(x)
dict_items([('brand', 'Ford'), ('model', 'Mustang'), ('year', 1964)])
def main():
    dir = dict(name='John', age=25, city='New York')
    for i in dir.items():
        print(i)
main()
('name', 'John')
('age', 25)
('city', 'New York')

Change items
Bạn có thể thay đổi giá trị của một mục cụ thể bằng cách tham chiếu đến khóa của nó.
def main():
    di = {
        "name": "John",
        "age": 30
    }
    di["age"] = 10
    print(di)
main()
{'name': 'John', 'age': 10}
update()
cập nhật phần tử với các mục từ đối số đã cho.
def main():
    di = {
        "name": "John",
        "age": 30,
        "address": "VietNam"
    }
    di.update({"age" : 40, "address": "USA"})
    print(di)
main()
{'name': 'John', 'age': 40, 'address': 'USA'}
Add items
Để thêm cặp key – value vào dictionary.
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict["color"] = "red"
print(thisdict)
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964, 'color': 'red'}
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict.update({"color": "red"})

print(thisdict)
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964, 'color': 'red'}
pop()
Để xóa mục có tên khóa được chỉ định.
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict.pop("model")
print(thisdict)
{'brand': 'Ford', 'year': 1964}
popitem()
Xóa một phần tử được chèn cuối cùng (trong các phiên bản trước 3.7, một phần tử ngẫu nhiên sẽ được xóa thay thế).
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict.popitem()
print(thisdict)
{'brand': 'Ford', 'model': 'Mustang'}
clear()
Để xóa sạch dictionary.
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict.clear()
print(thisdict)
{}
.copy()
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
mydict = thisdict.copy()
print(mydict)
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964}
