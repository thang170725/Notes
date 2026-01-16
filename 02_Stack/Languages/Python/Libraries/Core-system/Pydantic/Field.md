# Field
**Syn**
```bash
id: int = Field(
    default=, 
    gt=, # lớn hơn
    ge=, # lớn hơn hoặc bằng
    lt=, # nhỏ hơn
    le=, # nhỏ hơn hoặc bằng
    min_length=, # Độ dài tối thiểu.
    max_length=, # Độ dài tối đa.
    pattern= # Kiểm tra theo định dạng (Regex), ví dụ như số điện thoại hoặc mã định danh.
    )
```

# EmailStr
**Ex**
```python
from pydantic import BaseModel, Field, EmailStr
from typing import Optional

class User(BaseModel):
    id: int = Field(gt=0)
    username: str = Field(min_length=3, max_length=20)
    email: str = EmailStr
    age: Optional[int] = Field(ge=18)
    is_active: bool = True

user = User(
    id=1,
    username="thang123",
    email="thang@gmail.com",
    age=20
)

print(user)
```