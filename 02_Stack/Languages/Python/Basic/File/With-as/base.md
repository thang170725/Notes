# With … as
```bash
- with dùng để quản lý tài nguyên tự động:
    + Tự mở → tự đóng (file, database, network, lock…)
    + Tự giải phóng tài nguyên kể cả khi code bị lỗi
    + Không cần viết try / finally

- Nó hoạt động dựa trên giao thức context manager:
    + __enter__()
    + __exit__()
```
**Ex1: Không dùng with ... as**
```python
f = open("data.txt", "w")
f.write("hello")
f.close()  # nếu quên close → rò rỉ tài nguyên

# Nếu code bị lỗi trước khi close() → file không được đóng.
```
**Ex2: Có dùng with ... as**
```python
with open("data.txt", "w") as f:
    f.write("hello world")

# File tự đóng dù có lỗi trong block
```
**Ex3**
```python
with open("data.txt", "r", encoding="utf8") as f:
    content = f.read()
    print(content)

# Khi block with kết thúc → file tự đóng.
```
**Ex4**
```python
with open("input.txt") as inp, open("output.txt", "w") as out:
    for line in inp:
        out.write(line.upper())

# Rất tiện để xử lý nhiều file.
```