- [.new\_page()](#new_page)
  - [Demo cơ bản – mở tab mới\*\*](#demo-cơ-bản--mở-tab-mới)

---

# .new_page()
```bash
- Trong Playwright Python, new_page dùng để mở một tab (page) mới trong cùng một browser context.
```
**Sơ đồ**
```bash
browser
 └── context (cookie, session riêng)
      ├── page 1
      ├── page 2  ← new_page
      └── page 3
```
**Khi nào thì dùng new_page?**
```bash
- Website mở link sang tab mới
- Test nhiều user / nhiều màn hình trong cùng session
- So sánh dữ liệu giữa 2 trang
- Popup / OAuth / Payment / External link
```

## Demo cơ bản – mở tab mới**
```python
from playwright.async_api import async_playwright

async def demo():
    async with async_playwright() as p:
        browser = await p.chromium.launch(headless=False)
        context = await browser.new_context()

        page1 = await context.new_page()
        await page1.goto("https://example.com")

        # mở tab mới
        page2 = await context.new_page()
        await page2.goto("https://playwright.dev")

        await page1.wait_for_timeout(3000)

        await browser.close()

# 2 tab mở song song
# Dùng chung cookie / login
```