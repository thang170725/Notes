# zip()
**Ex1**
```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]

for values in zip(names, ages):
    print(values)
```
**Ex2**
```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]

combined = zip(names, ages) # zip hai list lại với nhau
print(list(combined)) # [('Alice', 25), ('Bob', 30), ('Charlie', 35)]

for name, age in zip(names, ages):
    print(f"{name} is {age} years old")

# Alice is 25 years old
# Bob is 30 years old
# Charlie is 35 years old
```
