# global
**Ex1: Không dùng global**
```python
count = 0

def increase():
    count += 1

increase() # lỗi
print(count)
```
**Ex2: Dùng global**
```python
count = 0

def increase():
    global count
    count += 1

increase() 
print(count) # 1
```