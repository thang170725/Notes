# ValueError
Lỗi giá trị, chuyển đổi giá trị.
## Bắt lỗi số nhập vào phải là số nguyên
```python
while True:
    try:
        a = int(input("Nhập số nguyên: "))
        break
    except ValueError:
        print("❌ Lỗi: phải nhập số nguyên")

```

# raise ValueError()
**Ex**
```python
def register(age: int):
    if age < 18:
        raise ValueError("Bạn chưa đủ 18 tuổi")
    print("Running ...")
register(15)

# Chủ động ném ra lỗi và dừng chương trình
```