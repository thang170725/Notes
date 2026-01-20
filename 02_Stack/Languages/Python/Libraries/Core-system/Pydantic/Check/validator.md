# @validator()
```bash
- Là hàm kiểm tra / chỉnh sửa dữ liệu trước khi model được tạo.
```
**Ex**
```python
from pydantic import BaseModel, validator

class User(BaseModel):
    username: str

    @validator("username")
    def check_username(cls, v):
        if len(v) < 3:
            raise ValueError("username quá ngắn")
        return v
```