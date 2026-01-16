# Xử lý số

## max() & min()
Tìm max, min của n số
**Cú pháp**
```text 
max(n1, n2, key= )
min(n1, n2, …)
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

## sum()
**EX**
```python
a = sum((1,2,3))
print(a)
```

## Bài tập
### Thuật toán tìm ước chung lớn nhất
```python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a
```
