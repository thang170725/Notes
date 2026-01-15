- [BaseModel](#basemodel)
  - [Bài tập](#bài-tập)
    - [Quản lý thông tin điện thoại](#quản-lý-thông-tin-điện-thoại)
- [Field](#field)
- [EmailStr](#emailstr)
- [@validator()](#validator)
- [@field\_validator()](#field_validator)
  - [Bài tập](#bài-tập-1)
    - [Demo](#demo)
- [@model\_validator()](#model_validator)
  - [Bài tập](#bài-tập-2)
    - [Demo](#demo-1)

---
```text
- Trong Python thông thường, bạn có thể truyền bất cứ thứ gì vào một đối tượng. Với Pydantic, bạn tạo ra một "khung bảo vệ". Dữ liệu đi vào phải đi qua cái khung này:
  + Nếu đúng kiểu: Nó được chấp nhận.
  + Nếu sai kiểu nhưng có thể sửa: Nó sẽ tự động được ép kiểu (ví dụ chuỗi "10" thành số 10).
  + Nếu sai hoàn toàn: Nó sẽ chặn lại và báo lỗi chi tiết.
- Cần pip install pydantic
- Pydantic là 'vị vua' trong thế giới API, nhưng ít khi được sử dụng trong lõi tính toán trong AI/Data Science
```

# BaseModel
- class nền của Pydantic, bạn kế thừa nó để tạo ra các “model dữ liệu”.
- Cần from pydantic import BaseModel

## Bài tập
### Quản lý thông tin điện thoại
**Code đúng chuẩn**
```python
from pydantic import BaseModel
from typing import List, Optional

class Product(BaseModel):
    id: int
    name: str
    price: float
    is_available: bool
    tags: List[str] = []
    discount: Optional[float] = None # có thể có hoặc không

data_ok = {
    "id": 1,
    "name": "iPhone 15",
    "price": 999.99,
    "is_available": True
}
p1 = Product(**data_ok)
print(f"Product 1: {p1.name} - {p1.price}$")
```

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

# @validator()
Là hàm kiểm tra / chỉnh sửa dữ liệu trước khi model được tạo.
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

# @field_validator()
Là hàm kiểm tra hoặc biến đổi dữ liệu của MỘT FIELD trước hoặc sau khi Pydantic gán vào model
**Syn**
```bash
@field_validator("username", mode="before")
- mode: quyết định validator chạy trước hay sau khi pydantic xử lý dữ liệu
```
## Bài tập
### Demo
```python
from pydantic import BaseModel, Field, field_validator
from typing import Optional

class User(BaseModel):
    username: str
    email: str = Field(pattern=r'^[\w\.]+@\w+\.\w+$')
    age: Optional[int] = Field(default=None, ge=18)
    is_active: bool = True

    @field_validator("username", mode="before")
    def check_username(cls, v):
        v = str(v).strip().lower()

        if " " in v:
            raise ValueError("username không được chứa khoảng trắng")

        if v == "admin":
            raise ValueError('username không được là "admin"')

        return v

    @field_validator("email")
    def check_email(cls, v):
        domain = v.split("@")[1]
        if domain not in {"gmail.com", "company.com"}:
            raise ValueError("Domain không được phép")
        return v

User( username=" ThangNguyen ", email="thang@gmail.com", age=20 )
```

# @model_validator()
Là validator chạy sau khi TẤT CẢ field đã hợp lệ → dùng để kiểm tra mối quan hệ giữa các field
**syn**
```bash
from pydantic import BaseModel, model_validator

class User(BaseModel):
    age: int

    @model_validator(mode="after")
    def check_model(self):
        return self
```
## Bài tập
### Demo
```python
from pydantic import BaseModel, Field, field_validator, model_validator
from typing import Optional

class User(BaseModel):
    username: str
    email: str = Field(pattern=r'^[\w\.]+@\w+\.\w+$')
    age: Optional[int] = Field(default=None, ge=18)
    is_active: bool = True
    is_young: bool = Field(default=False, exclude=True)

    @field_validator("username", mode="before")
    def check_username(cls, v):
        v = str(v).strip().lower()

        if " " in v:
            raise ValueError("username không được chứa khoảng trắng")

        if v == "admin":
            raise ValueError('username không được là "admin"')

        return v

    @field_validator("email")
    def check_email(cls, v):
        domain = v.split("@")[1]
        if domain not in {"gmail.com", "company.com"}:
            raise ValueError("Domain không được phép")
        return v

    @model_validator(mode="after")
    def check_model(self):
        # logic 1
        self.is_young = self.age is not None and self.age < 25

        # logic 2
        if self.is_active is False and self.age is None:
            raise ValueError("age must exist when user is inactive")

        # logic 3
        if self.username.startswith("test"):
            domain = self.email.split("@")[1]
            if domain != "company.com":
                raise ValueError("test users must use company.com email")

        return self
```