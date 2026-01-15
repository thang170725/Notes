# page.is_visible() & page.is_enabled() & locator.is_visible()
# page.text_content() & page.inner_text() 
 NHÓM DEBUG – HỌC NHANH X10. Khi mới học → luôn bật.

# page.pause() # slow_mo # print()
## pause để xem từng bước
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(
        headless=False,
        slow_mo=500  # chậm từng hành động
    )

    page = browser.new_page()
    page.goto("https://google.com")

    # Dừng lại để inspect
    page.pause()

    browser.close()
```
- NHÓM CHUỘT & BÀN PHÍM – GIỐNG NGƯỜI THẬT. Dùng để vượt web khó

# page.mouse.move() & page.mouse.click() & page.keyboard.press()
## di chuyển chuột
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()

    page.goto("https://example.com")

    # Di chuyển chuột tới tọa độ
    page.mouse.move(400, 300)

    # Click chuột trái
    page.mouse.click(400, 300)

    page.wait_for_timeout(3000)
    browser.close()
```