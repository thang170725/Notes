# BaseModel
```bash
- class nền của Pydantic, bạn kế thừa nó để tạo ra các “model dữ liệu”.
- Cần from pydantic import BaseModel
```
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
    "id": 1, # thay bằng 'a' -> báo lỗi
    "name": "iPhone 15",
    "price": 999.99,
    "is_available": True
}
p1 = Product(**data_ok)
print(f"Product 1: {p1.name} - {p1.price}$")
```