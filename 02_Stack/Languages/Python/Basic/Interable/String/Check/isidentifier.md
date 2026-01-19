# .isidentifier()
```bash
- Trả về True nếu chuỗi là một định danh hợp lệ, nếu không thì trả không thì trả về false.
- Một chuỗi được coi là một định danh hợp lệ nếu nó chỉ chứa các chữ cái và các chữ số hoặc dấu gạch dưới. 
- Một định danh hợp lệ không thể bắt đầu bằng một số hoặc chứa bất kỳ khoảng trắng nào.
```
**Syn** 
```bash
<variable>.isidentifier()
```
**Ex**
```python
tests = [
    "name",
    "_age",
    "user1",
    "1user",
    "user-name",
    "class",
    "user name"
]

for t in tests:
    print(t, "->", t.isidentifier())

# name        -> True
# _age        -> True
# user1       -> True
# 1user       -> False
# user-name   -> False
# class       -> True   ❗
# user name   -> False
```