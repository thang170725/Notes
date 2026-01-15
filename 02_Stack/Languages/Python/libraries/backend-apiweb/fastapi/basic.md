- [APIRouter](#apirouter)
- [Depends()](#depends)
  - [.include\_router()](#include_router)
    - [get data](#get-data)
      - [Demo cấu trúc chuẩn cho get data json](#demo-cấu-trúc-chuẩn-cho-get-data-json)

---

- FastAPI nhanh hơn Flask rất nhiều. FastAPI được build trên ASGI (uvicorn / starlette) → có async/await thật sự, xử lý hàng nghìn request/giây.
- Benchmark
  + Flask: 3.000–4.000 req/s
  + FastAPI: 10.000–20.000 req/s
  + FastAPI dùng Pydantic, tự động: validate dữ liệu, parse JSON, convert types, báo lỗi rõ ràng
- Cần pip install fastapi uvicorn

# APIRouter
- APIRouter = Thay vì viết tất cả API trong main.py, ta nhóm lại
- Lợi ích: Code gọn, Dễ mở rộng, Chuẩn kiến trúc (layered / clean)
**Syn**
```bash
router = APIRouter(prefix="/user", tags=["User"])
- prefix="/user": @router.get("/data-left") -> URL thực tế /user/data-left
    + Tránh lặp /user ở từng route
    + Dễ versioning (/api/v1/user)
- tags=["User"]: Chỉ dùng cho Swagger UI /docs
    + Nó giúp: nhóm API, dễ đọc, không ảnh hưởng runtime
```

# Depends()
FastAPI tự tạo & quản lý phụ thuộc cho bạn.
**Ex**
```python
def get_user_service():
    return UserService()

@router.get("/data")
def data(service: UserService = Depends(get_user_service)):
    ...
# FastAPI sẽ:
# Gọi get_user_service()
# Truyền kết quả vào service
# Tại sao không viết thẳng? service = UserService()  # ❌
# Vì: Dễ test, Dễ mock, Dễ đổi implementation sau này, Chuẩn kiến trúc Clean Architecture
```

## .include_router()
Gắn router vào app
```python
app.include_router(user.router)
# Mọi route trong user.router sẽ hoạt động
```

### get data 
#### Demo cấu trúc chuẩn cho get data json
**tại backend/app/service/user_service.py**
```bash
- folder service sẽ chứa business logic (db, AI, ML, ...)
```
```python
class UserService:
    async def get_data_left(self) -> str:
        return "this data is on the left"

    async def get_data_right(self) -> str:
        return "this data is on the right"
```
**tại backend/app/routers/user.py**
trong routers nên tạo thêm file __init__.py kể cả rỗng để tránh lỗi (from .user import router)
```python
from fastapi import APIRouter, Depends
from backend.app.services.user_service import UserService

router = APIRouter(prefix="/user", tags=["User"])

def get_user_service() -> UserService:
    return UserService()

@router.get("/data-left")
async def data_left(service: UserService = Depends(get_user_service)):
    return {"data": await service.get_data_left()}

@router.get("/data-right")
async def data_right(service: UserService = Depends(get_user_service)):
    return {"data": await service.get_data_right()}
```
**tại backend/app/main**
```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

from backend.app.routers import user

def create_app() -> FastAPI:
    app = FastAPI(
        title="Backend API",
        version="1.0.0",
        docs_url="/docs",
        redoc_url="/redoc",
    )

    # CORS
    app.add_middleware(
        CORSMiddleware,
        allow_origins=["*"],
        allow_methods=["*"],
        allow_headers=["*"],
    )

    # Routers
    app.include_router(user.router)

    return app

app = create_app()
```
# UploadFile + File() & .read()
Đại diện cho file được upload từ form-data
**Syn**
```bash
image: UploadFile = File(...)
- File(...) → bắt buộc phải có.
- UploadFile → FastAPI xử lý stream (tốt hơn bytes).
- <input type="file" name="image"> name="image" PHẢI TRÙNG với biến image.
```
**Ex**
```python
from fastapi import APIRouter, UploadFile, File, Depends
from fastapi.responses import Response
from backend.app.services.user_service import UserService

router = APIRouter(prefix="/user", tags=["User"])

def get_user_service() -> UserService:
    return UserService()

@router.post("/image-grayscale")
async def image_grayscale(
    image: UploadFile = File(...),
    service: UserService = Depends(get_user_service)
):
    image_bytes = await image.read() # bytes, Đây chính là: PNG / JPG raw bytes, Chưa decode, Chưa là numpy, Chưa là ảnh OpenCV
    result_bytes = await service.grayscale_image(image_bytes=image_bytes)

    return Response(
        content=result_bytes,
        media_type='image/png'
    )
```
# Response
- cần from fastapi.responses import Response
- Khi nào dùng Response? Khi KHÔNG trả JSON
- Bạn đang trả: bytes, ảnh PNG -> bắt buộc dùng Response