# Nhập một số nguyên có ít hơn 5 chữ số
```python
num = None
while True:
    val = input('Input: ')
    
    if val.isdigit() and len(val) < 5:
        num = int(val)
        break
    else:
        print('Input must be Integer!!!')

print(num)

# isdigit không xử lý được số âm (-123) nếu nhập vào số âm sẽ cho ra kết quả sai.
# nếu vẫn muốn dùng isdigit cần xử lý thêm trường hợp số âm.
```