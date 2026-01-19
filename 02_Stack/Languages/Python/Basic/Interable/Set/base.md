```bash
- Các mục set không được sắp xếp theo thứ tự, không thể thay đổi và không cho phép các giá trị trùng lặp.
- Sử dụng set để:
    + Loại bỏ các phần tử trùng lặp.
    + Kiểm tra sự tồn tại của một phần tử.
    + Thực hiện các phép toán tập hợp.
    + Lưu trữ dữ liệu không có thứ tự và duy nhất.
    + Tối ưu hóa hiệu năng.
```
**Syn**
```bash
<variable> = {value1, value2, …}
<variable> = set((value1, value2, …))
```
**Ex**
```python
thisset = {"apple", "banana", "cherry", True, 1, 2}
print(thisset)

# {True, 2, 'apple', 'banana', 'cherry'}
# 1 không xuất hiện vì nó coi 1 và true là phần tử trùng lặp.
```