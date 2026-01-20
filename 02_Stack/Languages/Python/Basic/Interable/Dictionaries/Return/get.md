# .get()
```bash
Để trả về value của một key nào đó.
```
**Syn**
```bash
<variable>.get(<key>, default)

- Nếu key chưa có thì trả về giá trị defaule
```
**Ex1**
```python
dir = dict(name='John', age=25, city='New York')
print(dir.get('name')) # John
```
**Ex2: Đếm số lượng phần tử**
```python
labels = ['no', 'no']
counts = {}
for label in labels:
    counts[label] = counts.get(label, 0) + 1 
print(counts)
{'no': 2}
```