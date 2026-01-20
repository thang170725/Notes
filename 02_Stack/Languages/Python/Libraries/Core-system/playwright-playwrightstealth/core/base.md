- [Set up](#set-up)
- [gencode](#gencode)
  - [Mở firefox và vào Google](#mở-firefox-và-vào-google)
- [mở web bằng profile thật](#mở-web-bằng-profile-thật)

---

```bash
Để hiểu cách hoạt động của Playwright một cách đơn giản nhất, bạn có thể tưởng tượng nó như một người dùng thật: Mở trình duyệt -> Đợi trang hiện ra -> Tìm thứ mình cần -> Lấy thông tin.
```
# Set up
```bash
pip install playwright
playwright install
```

# gencode
```bash
- playwright codegen https://example.com
- playwright codegen --target python https://youtube.com
```

# khi nào thì dùng playwright.async_api, sync_api
```bash
Playwright Python có 2 cách dùng:
API	        Cách chạy	                Đặc điểm
async_api	Bất đồng bộ (async/await)	Mạnh, nhanh, chuyên nghiệp
sync_api	Đồng bộ (chạy từng bước)	Dễ học, dễ đọc
```
**Ex**
```bash
- Sync (đồng bộ): Làm xong việc A → mới làm B
    1. Đi mua cà phê
    2. Uống xong
    3. Rồi mới đi làm
- Async (bất đồng bộ). Trong lúc chờ A → có thể làm B
    1. Order cà phê
    2. Trong lúc chờ → check mail
    3. Cà phê xong → uống
```
**Khi nào dùng sync_api?**
```bash
- Mới học Playwright
- Viết script đơn giản
- Debug test
- Test nhỏ, chạy local
- Không cần chạy song song
- Ưu điểm:
    + Code dễ đọc
    + Ít lỗi logic
    + Không cần async / await
```
**Khi nào dùng async_api?**
```bash
- Project lớn
- Chạy nhiều test
- Cần chạy song song
- Tích hợp CI/CD
- Kết hợp với framework async (FastAPI, asyncio)
- Ưu điểm:
    + Nhanh hơn
    + Scale tốt
    + Chuẩn production
```

## Mở firefox và vào Google
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.firefox.launch(
        headless=False 
    )

    context = browser.new_context()

    page = context.new_page()
    page.goto("https://www.google.com")
    page.wait_for_timeout(5000)

    browser.close()
```

# mở web bằng profile thật
Cách setup profile thật [link](../base.md)
```python
from playwright.sync_api import sync_playwright

USER_DATA_DIR = "/home/thang/pw-firefox-profile"

with sync_playwright() as p:
    context = p.firefox.launch_persistent_context(
        user_data_dir=USER_DATA_DIR,
        headless=False
    )

    page = context.pages[0]
    page.goto("https://batdongsan.com.vn/nha-dat-ban-ha-noi")

    print("👉 Login xong rồi quay lại terminal nhấn Enter") # sau khi login xong, Enter mới đóng
    input()
```