# max() 
```bash
- Tìm max của một danh sách.
```
**Syn**
```bash
max(n1, n2, key= )
```
**Ex**
```python
print(max(1,2,3)) 
print(max([1,2,3]))
```
**EX1**
```python
labels = ['a', 'b', 'c', 'a', 'b', 'a']
print(max(set(labels), key=labels.count))
my_dict = {'a': 10, 'b': 50, 'c': 25}
```
**EX2**
```python
max_key = max(my_dict, key=my_dict.get) # Lấy Key có Value lớn nhất
max_value = my_dict[max_key] # Lấy Value tương ứng

print(f"Key lớn nhất là: {max_key}, Value là: {max_value}") # Kết quả: Key lớn nhất là: b, Value là: 50
```