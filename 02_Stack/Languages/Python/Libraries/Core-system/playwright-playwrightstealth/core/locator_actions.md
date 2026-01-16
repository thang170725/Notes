```text
NHÓM TƯƠNG TÁC – GÕ, CLICK NHƯ NGƯỜI. Nhóm dùng hàng ngày
```

# .click()
**Ex**
```python
page.get_by_role("button", name="Login").click() # click nút login
```

# .fill() 
**Ex**
```python
page.get_by_role("textbox", name="Email").fill("test@gmail.com")
page.get_by_role("textbox", name="Password").fill("123456")
```

# .check()
**Ex**
```python
page.get_by_role("checkbox", name="Remember me").check()
```
& page.type() & page.press()
## search google
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()

    page.goto("https://www.google.com")
    page.wait_for_selector("textarea[name='q']")

    # Điền nội dung (xóa text cũ)
    page.fill("textarea[name='q']", "Playwright python")

    # Nhấn Enter
    page.press("textarea[name='q']", "Enter")

    page.wait_for_timeout(5000)
    browser.close()
```
- NHÓM LẤY DỮ LIỆU (SCRAPING). Crawl dữ liệu web


& locator.all_inner_texts() & locator.get_attribute()
## Lấy tiêu đề trang
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch()
    page = browser.new_page()

    page.goto("https://example.com")

    # Lấy text thẻ h1
    title = page.text_content("h1")

    print("Tiêu đề:", title)

    browser.close()
```