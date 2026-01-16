# Nhập số nguyên nhỏ hơn 5 chữ số
```python
while True:
    num_str = input("Nhập số nguyên 5 chữ số: ")
    try:
        num = int(num_str) # Thử ép kiểu, nếu là chữ sẽ nhảy xuống except
        if len(num_str) == 5:
            break
        else:
            print("Lỗi: Phải nhập đúng 5 chữ số!")
    except ValueError:
        # Lỗi này xảy ra khi người dùng nhập chữ (ví dụ: "abc")
        print("Lỗi: Đây không phải là số nguyên!")

print(f"Số bạn đã nhập: {num}")
```