- [.launch\_persistent\_context() \& .new\_page() \& .goto() \& .close()](#launch_persistent_context--new_page--goto--close)
- [sync\_playwright() \& p.chromium.launch() \& browser.new\_context() \&](#sync_playwright--pchromiumlaunch--browsernew_context-)
  - [Mở firefox và vào Google](#mở-firefox-và-vào-google)
  - [mở web bằng browser bất kỳ](#mở-web-bằng-browser-bất-kỳ)

---

```text
- Nhóm khởi tạo, dùng để mở trình duyệt
- Các website hiện đại đều có cơ chế chống bot vô cùng mạnh nên cần một số kỹ thuật mới có thể crawl dữ liệu thành công.
```

# .launch()

# .launch_persistent_context()
```bash
- Đây là cách sử dụng profile thật để chống bot.
```
**Syn**
```bash
context = p.chromium.launch_persistent_context(
    user_data_dir="/home/thang/pw-chrome-profile",
    headless=False,
    args=[
            "--disable-blink-features=AutomationControlled",
            "--start-maximized"
    ]
)
- args: dòng đầu để che navigator.webdriver, dòng 2 chỉ để mở cửa sổ to.
```




