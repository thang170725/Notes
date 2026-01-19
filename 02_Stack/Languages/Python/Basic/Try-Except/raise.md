# raise ValueError()
```bash
Chủ động ném ra lỗi và dừng chương trình.
```
**Ex**
```python
def register(age: int):
    if age < 18:
        raise ValueError("Bạn chưa đủ 18 tuổi")
    print("Running ...")
register(15)
```