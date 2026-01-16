- NHÓM CHỜ (WAIT) – KHÔNG CÓ LÀ TOANG. Web hiện đại load bằng JS → bắt buộc phải chờ.
- Không wait → lỗi random. wait_for_selector là dùng nhiều nhất

# page.wait_for_selector() & page.wait_for_timeout() & page.wait_for_load_state()
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()

    page.goto("https://www.google.com")

    # Chờ element xuất hiện trên DOM
    page.wait_for_selector("textarea[name='q']")

    print("Ô tìm kiếm đã sẵn sàng")

    page.wait_for_timeout(3000)
    browser.close()
```