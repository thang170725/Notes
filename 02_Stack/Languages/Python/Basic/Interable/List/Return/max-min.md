# max() 
```bash
- Tìm max của một danh sách.
```
**Syn**
```bash
max(n1, n2, key= )
```
**Ex1**
```python
print(max(1,2,3)) 
print(max([1,2,3]))
```
**EX2**
```python
my_dict = {'a': 10, 'b': 50, 'c': 25}

max_key = max(my_dict, key=my_dict.get) # Lấy Key có Value lớn nhất
max_value = my_dict[max_key] # Lấy Value tương ứng

print(f"Key lớn nhất là: {max_key}, Value là: {max_value}") # Kết quả: Key lớn nhất là: b, Value là: 50
```