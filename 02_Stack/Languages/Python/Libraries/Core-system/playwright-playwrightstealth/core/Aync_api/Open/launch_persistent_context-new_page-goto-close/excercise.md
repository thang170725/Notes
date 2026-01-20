# mở các tab mới
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
        await browser.close()

# 2 tab mở song song
# Dùng chung cookie / login
```