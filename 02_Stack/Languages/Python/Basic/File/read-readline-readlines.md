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
```bash
Đọc nội dung file theo dòng. Chỉ đọc một dòng.
```
**Syn**
```bash
<variable>.readline()
```
**Ex**
```python
txt = open("E:\\Python\Text.txt", "rt")
print(txt.readline()) # Hello
txt.close()
```

# .readlines()
```bash
Tạo ra một mảng. Mỗi dòng trong file sẽ tương ứng với một phần tử trong mảng.
```
**Syn**
```bash
<variable>.readlines()
```
**Ex**
```python
txt = open("E:\\Python\Text.txt", "rt")
print(txt.readlines()) # ['Hello\n', 'My name is Thang\n', 'I am from VietNam']
txt.close()
```