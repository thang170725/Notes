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

khi nào thì dùng playwright.async_api, sync_api

Câu hỏi này rất hay 👍 vì nhiều người mới dùng Playwright hay bị rối chỗ async_api vs sync_api.

Mình giải thích dễ hiểu – thực tế – có ví dụ nhé.

1. playwright.async_api và sync_api là gì?

Playwright Python có 2 cách dùng:

API	Cách chạy	Đặc điểm
async_api	Bất đồng bộ (async/await)	Mạnh, nhanh, chuyên nghiệp
sync_api	Đồng bộ (chạy từng bước)	Dễ học, dễ đọc
2. Hiểu đơn giản bằng ví dụ đời thường 🧠
Sync (đồng bộ)

Làm xong việc A → mới làm B

Ví dụ:

Đi mua cà phê

Uống xong

Rồi mới đi làm

Async (bất đồng bộ)

Trong lúc chờ A → có thể làm B

Ví dụ:

Order cà phê

Trong lúc chờ → check mail

Cà phê xong → uống

3. Khi nào dùng sync_api? ✅
👉 DÙNG khi:

Mới học Playwright

Viết script đơn giản

Debug test

Test nhỏ, chạy local

Không cần chạy song song

Ví dụ sync_api
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()

    page.goto("https://example.com")
    page.click("text=More information")

    browser.close()


📌 Ưu điểm:

Code dễ đọc

Ít lỗi logic

Không cần async / await

4. Khi nào dùng async_api? 🚀
👉 DÙNG khi:

Project lớn

Chạy nhiều test

Cần chạy song song

Tích hợp CI/CD

Kết hợp với framework async (FastAPI, asyncio)

Ví dụ async_api
import asyncio
from playwright.async_api import async_playwright

async def run():
    async with async_playwright() as p:
        browser = await p.chromium.launch(headless=False)
        page = await browser.new_page()

        await page.goto("https://example.com")
        await page.click("text=More information")

        await browser.close()

asyncio.run(run())


📌 Ưu điểm:

Nhanh hơn

Scale tốt

Chuẩn production

5. So sánh nhanh 🔍
Tiêu chí	sync_api	async_api
Dễ học	⭐⭐⭐⭐⭐	⭐⭐
Dễ debug	⭐⭐⭐⭐⭐	⭐⭐
Hiệu năng	⭐⭐	⭐⭐⭐⭐⭐
Chạy song song	❌	✅
CI/CD	⚠️	✅
6. Có được trộn sync và async không? ❌

🚫 KHÔNG

from playwright.sync_api import Page
from playwright.async_api import Browser


👉 Dễ crash, bug khó tìm

7. Rule of Thumb (quy tắc nhớ nhanh)

🟢 Học / script nhỏ → sync_api
🔵 Project lớn / chạy nhiều test → async_api

8. Dùng trong test framework
Pytest + sync
def test_homepage(page):
    page.goto("https://example.com")

Pytest + async
@pytest.mark.asyncio
async def test_homepage(page):
    await page.goto("https://example.com")

Tóm lại 1 câu

sync_api để học và viết nhanh, async_api để scale và chạy mạnh 💪

Nếu bạn muốn, mình có thể:

Giúp bạn chuyển code sync → async

So sánh performance thực tế

Gợi ý dùng pytest-playwright

Chỉ ra lỗi thường gặp khi dùng async

Bạn đang viết test cá nhân hay project team?

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