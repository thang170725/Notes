- [Cài đặt](#cài-đặt)
- [Depends()](#depends)
  - [.include\_router()](#include_router)
    - [get data](#get-data)
      - [Demo cấu trúc chuẩn cho get data json](#demo-cấu-trúc-chuẩn-cho-get-data-json)
- [UploadFile + File() \& .read()](#uploadfile--file--read)
- [Response](#response)
---
# Cài đặt & run chương trình
```bash
- pip install fastapi uvicorn
- uvicorn backend.api.register:app --reload --port 3651 (để chạy chương trình)
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