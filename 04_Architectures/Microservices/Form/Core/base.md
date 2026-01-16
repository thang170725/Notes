```bash
- “file trong core là những file khi bỏ đi sẽ ảnh hưởng trực tiếp đến dự án”
- Core = thứ mà nếu mất nó, hệ thống không còn là chính nó nữa
```
**Áp vào project housePrice**
```bash
Thành phần	Bỏ đi	Dự án còn chạy không
db.py	    ❌	        ❌
queries.py	❌	        ❌
tables.py	❌	        ❌
Crawl	    ❌	        ✅ (lấy tay, CSV, API)

⇒ Crawl không phải core
```
**Ví dụ đời thực**
```bash
Nhà 🏠
Thứ	Vai trò
Móng	core
Cột	core
Tường	core
Cửa sổ	thay được
Rèm	thay được

⇒ Crawl = cửa sổ / rèm
⇒ DB + query = móng + cột
```