# .items()
```bash
- Dùng để lấy ra các cặp key, value. Thường dùng trong vòng lặp để lặp qua các key, value. 
- Phương thức này trả về từng mục trong từ điển dưới dạng các bộ trong danh sách.
```
**Syn**
```bash
<variable>.items()
```
**Ex1**
```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
x = thisdict.items()
print(x) # dict_items([('brand', 'Ford'), ('model', 'Mustang'), ('year', 1964)])
```
**Ex2**
```python
def main():
    dir = dict(name='John', age=25, city='New York')
    for i in dir.items():
        print(i)
main()

# ('name', 'John')
# ('age', 25)
# ('city', 'New York')
```