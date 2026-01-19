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