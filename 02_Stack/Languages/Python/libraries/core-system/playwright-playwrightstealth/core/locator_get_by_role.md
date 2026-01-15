```text
- get_by_role là cách chọn (locator) “xịn” nhất của Playwright, dựa trên ARIA accessibility role thay vì CSS/XPath. Nó ổn định – ít vỡ – giống cách người dùng thật tương tác.
- get_by_role dùng để tìm element theo vai trò (role) giao diện, ví dụ: button, textbox, ...
- Nó không phụ thuộc class/id → web đổi CSS vẫn chạy.
- Vấn đề: Dev đổi class → chết, XPath -> Dài, khó đọc
-> get_by_role: Chuẩn web, ổn định. Playwright khuyên dùng số 1
```
**Syn**
```bash
page.get_by_role(role, **options)
- role
    + button    : nút
    + textbox	: input text
    + link	    : thẻ a
    + heading   : h1–h6
    + checkbox	: checkbox
    + radio	    : radio
    + combobox	: select
    + menuitem	: item menu
    + dialog	: modal
```

## Mở youtube -> search -> click -> skip ads
```python
from playwright.sync_api import sync_playwright
import re

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()

    page.goto("https://www.youtube.com/")

    search = page.get_by_role("combobox", name="Search")
    search.fill("list edm hot tiktok")
    search.press("Enter")

    # đợi list video load
    page.wait_for_selector("ytd-video-renderer")

    first_video = page.locator("ytd-video-renderer").first
    first_video.scroll_into_view_if_needed()
    first_video.click()

    # đợi video player
    page.wait_for_selector("video")

    try:
        skip = page.get_by_role(
            "button",
            name=re.compile("Skip|Bỏ qua", re.I)
        )
        skip.wait_for(timeout=35000)
        skip.click()
    except:
        print("Không có quảng cáo hoặc không skip được")


    page.keyboard.press("Enter")

    input("👉 Nhấn Enter để đóng browser...")
    browser.close()
```