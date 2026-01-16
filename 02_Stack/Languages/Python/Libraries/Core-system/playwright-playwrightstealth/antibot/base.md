- [Cách vượt cloudfare](#cách-vượt-cloudfare)

---

```bash
- Các hành vi né bot
    + persistent profile
    + stealth
    + hành vi người thật
```

# Cách vượt cloudfare
```text
luôn luôn truy cập vào trang web 1 lần trước để giải hết capcha.
```
**Step 1**
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch_persistent_context(
        user_data_dir="/home/thang/pw-chrome-profile",
        headless=False,
        args=[
            "--disable-blink-features=AutomationControlled",
            "--start-maximized"
        ]
    )

    page = browser.new_page()
    page.goto("https://batdongsan.com.vn")

    input("👉 Giữ browser mở. Khi bạn xác minh xong Cloudflare thì nhấn Enter...")
    browser.close()
```
**Step 2**
```text
gen code hoặc tự việt code.
```







