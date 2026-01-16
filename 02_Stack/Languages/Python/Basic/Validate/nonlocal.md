# nonlocal
**Ex**
```python
def outer():
    x = 10

    def inner():
        nonlocal x
        x += 1
        print(x)

    inner()
```