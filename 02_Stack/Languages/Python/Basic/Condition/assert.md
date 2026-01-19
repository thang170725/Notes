# assert
```bash
- Một cách để kiểm tra điều kiện, nếu điều kiện không đúng, Python sẽ ném ra AssertionError và có thể kèm thông điệp tùy chỉnh. Nó rất hữu ích để debug hoặc bảo vệ code khỏi dữ liệu sai.
```
**Syn**
```bash
assert condition, "Thông báo nếu điều kiện sai"
    + condition: biểu thức boolean bạn muốn kiểm tra (True hoặc False)
    + Nếu condition = True → code tiếp tục chạy bình thường
    + Nếu condition = False → ném AssertionError kèm thông báo
```
**Ex**
```python
x = 5
assert x > 0, "x phải lớn hơn 0"
print("Code tiếp tục chạy bình thường")
```
