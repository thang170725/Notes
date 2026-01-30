- [model\_dump()](#model_dump)
---
# model_dump()
```bash
- Chuyển object Pydantic → dict Python
- Dùng khi bạn muốn:
    + Trả JSON cho API
    + Ghi DB
    + Log dữ liệu
    + Gửi dữ liệu sang service khác
```
**Syn**
```bash
data = user.model_dump(
    exclude_none=True,
    include={"id", "name"},
    exclude={"age"},
    mode="json"
)

- exclude_none  : Loại bỏ phần tử có giá trị là None
- include       : chỉ lấy một vài field
- exclude       : bỏ một vài field
- mode          : trả về một định dạng
```
**Ex**
```python
from pydantic import BaseModel

class User(BaseModel):
    id: int
    name: str
    age: int | None = None

user = User(id=1, name="Thắng", age=25)

data = user.model_dump()
print(data)


# {
#     'id': 1,
#     'name': 'Thắng',
#     'age': 25
# }
```