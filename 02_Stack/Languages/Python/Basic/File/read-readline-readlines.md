# .read()
```bash
Dùng để đọc nội dung một file.
```
**Syn**
```bash
name.read(n)
    + n: Đọc ra n nội dụng. Không truyền tham số gì mặc định là đọc toàn bộ file
```
**Ex**
```python
txt = open("E:\\Python\Text.txt", "rt")
print(txt.read()) # Hello world, i am Thang and i am coder, welcome to my world,
txt.close()
```

# .readline()
Đọc nội dung file theo dòng. Chỉ đọc một dòng.
Cú pháp: 
<variable>.readline()

txt = open("E:\\Python\Text.txt", "rt")
print(txt.readline())
txt.close()
Hello
.readlines()
Tạo ra một mảng. Mỗi dòng trong file sẽ tương ứng với một phần tử trong mảng.
Cú pháp: 
<variable>.readlines()

txt = open("E:\\Python\Text.txt", "rt")
print(txt.readlines())
txt.close()
['Hello\n', 'My name is Thang\n', 'I am from VietNam']