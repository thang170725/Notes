- [Nhập số nguyên nhỏ hơn 5 chữ số](#nhập-số-nguyên-nhỏ-hơn-5-chữ-số)
- [Nhập vào hai số nguyên S và E, quy định S \< E và E không quá 8 chữ số.](#nhập-vào-hai-số-nguyên-s-và-e-quy-định-s--e-và-e-không-quá-8-chữ-số)

---

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

# Nhập vào hai số nguyên S và E, quy định S < E và E không quá 8 chữ số.
```python
while True:
    SE_STR = input("S and E: ").split()
    try:
        SE = list(map(int, SE_STR))
   
        S, E = SE[0], SE[1]
        if len(str(E)) < 8 and (S < E):
            break 
    except ValueError:
        print("Error, Please again!!!")
```