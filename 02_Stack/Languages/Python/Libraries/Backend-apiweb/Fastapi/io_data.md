- [FastAPI() \& add\_middleware](#fastapi--add_middleware)
  - [lấy data Json từ client](#lấy-data-json-từ-client)
- [APIRouter() \& .include\_router() \& create\_app()](#apirouter--include_router--create_app)
  - [lấy data Json từ client](#lấy-data-json-từ-client-1)
---
# FastAPI() & add_middleware
## lấy data Json từ client 
```python
from backend.schemas.user import UserSchema
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["*"],
    allow_headers=["*"],
)

@app.post('/register')
async def fetch_data(user: UserSchema):
    print(user)

    return {
        'message': "user received",
        'data': user
    }
```
# APIRouter() & .include_router() & create_app()
```bash
- APIRouter         : Thay vì viết tất cả API trong main.py, ta nhóm lại để code gọn, Dễ mở rộng, Chuẩn kiến trúc (layered / clean).
- .include_router() : Gắn router vào app
```
**Syn: APIRouter**
```bash
router = APIRouter(prefix="/user", tags=["User"])

- prefix="/user": @router.get("/data-left") -> URL thực tế /user/data-left
    + Tránh lặp /user ở từng route
    + Dễ versioning (/api/v1/user)
- tags=["User"]: Chỉ dùng cho Swagger UI /docs
    + Nó giúp: nhóm API, dễ đọc, không ảnh hưởng runtime
```
## lấy data Json từ client
```bash
backend/
├── app.py   
├── api    
├    └── register.py
```
**app.py**
```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

from backend.api import register 

def create_app() -> FastAPI:
    app = FastAPI(
        title="Backend API",
        version="1.0.0", 
    )

    # CORS
    app.add_middleware(
        CORSMiddleware,
        allow_origins=["*"],
        allow_methods=["*"],
        allow_headers=["*"],
    )

    # Routers
    app.include_router(register.router)

    return app

app = create_app()
```
**register.py**
```python
from backend.schemas.user import UserSchema
from fastapi import APIRouter

router = APIRouter(prefix="/register", tags=["Register"])

@router.post('')
async def fetch_data(user: UserSchema):
    print(user)

    return {
        'message': "user received",
        'data': user
    }
```