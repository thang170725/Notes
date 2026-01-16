# Demo ví dụ về wait_for_select
```bash
Dưới đây là ví dụ kết hợp các hàm cơ bản nhất với wait_for_selector. Ví dụ này sẽ truy cập vào trang Wikipedia, đợi ô tìm kiếm xuất hiện và lấy nội dung tiêu đề trang.Code Demo tối giảnPythonimport asyncio
```
```python
from playwright.async_api import async_playwright

async def run():
    async with async_playwright() as p:
        # 1. Mở trình duyệt
        browser = await p.chromium.launch(headless=False)
        page = await browser.new_page()

        # 2. Đi tới trang web
        await page.goto("https://vi.wikipedia.org/")

        # 3. Đợi cho đến khi phần tử "Tiêu đề chào mừng" xuất hiện trên màn hình
        # Class CSS của tiêu đề Wikipedia là '#mp-welcome'
        await page.wait_for_selector("#mp-welcome")

        # 4. Tìm phần tử đó bằng locator
        welcome_msg = page.locator("#mp-welcome")

        # 5. Lấy nội dung chữ và in ra
        text = await welcome_msg.inner_text()
        print(f"Nội dung tìm được: {text}")

        # Đóng trình duyệt
        await browser.close()

asyncio.run(run())
```