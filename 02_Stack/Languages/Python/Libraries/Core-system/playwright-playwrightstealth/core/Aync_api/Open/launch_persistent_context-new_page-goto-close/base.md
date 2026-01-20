- [.launch\_persistent\_context()](#launch_persistent_context)

---

**Sơ đồ**
```bash
browser
 └── context (cookie, session riêng)
      ├── page 1
      ├── page 2  ← new_page
      └── page 3
```

# .launch_persistent_context()
```bash
- Đây là cách sử dụng profile thật để chống bot.
- Các website hiện đại đều có cơ chế chống bot vô cùng mạnh nên cần một số kỹ thuật mới có thể crawl dữ liệu thành công.
```
**Syn**
```bash
browser = p.chromium.launch_persistent_context(
    user_data_dir="/home/thang/pw-chrome-profile",
    headless=False,
    args=[
            "--disable-blink-features=AutomationControlled",
            "--start-maximized"
    ]
)

- args: dòng đầu để che navigator.webdriver, dòng 2 chỉ để mở cửa sổ to.
```
# .new_page()
```bash
- Trong Playwright Python, new_page dùng để mở một tab (page) mới trong cùng một browser context.
```
**Khi nào thì dùng new_page?**
```bash
- Website mở link sang tab mới
- Test nhiều user / nhiều màn hình trong cùng session
- So sánh dữ liệu giữa 2 trang
- Popup / OAuth / Payment / External link
```

# page.goto()
```bash
- Tác dụng: Điều hướng trình duyệt đến một trang web cụ thể.
- Nó có các tham số (parameters) rất quan trọng để giúp bạn kiểm soát việc "Khi nào thì coi như trang web đã tải xong?".
```
**Syn**
```bash
await page.goto("đường_dẫn_url")
- url (Bắt buộc)    : Địa chỉ trang web bạn muốn truy cập. Lưu ý: Phải có đầy đủ giao thức http:// hoặc https://
- wait_until (Quan trọng nhất): Đây là tham số quyết định Playwright sẽ đợi đến thời điểm nào thì mới chạy câu lệnh tiếp theo. 
    + 'domcontentloaded': Đợi cho đến khi cấu trúc HTML được tải xong.Khi bạn chỉ cần lấy chữ, không quan tâm đến ảnh hay CSS. Rất nhanh.
    + 'load' (Mặc định): Đợi cho đến khi toàn bộ trang web, ảnh, và các file CSS tải xong. Khi trang web đơn giản, không có nhiều hiệu ứng phức tạp.
    + 'networkidle' : Đợi cho đến khi không còn yêu cầu mạng nào trong ít nhất 500ms. Nên dùng: Khi trang web dùng Javascript để tải dữ liệu (như Facebook, Shopee, Batdongsan).
- timeout: Thời gian tối đa (tính bằng mili giây) mà Playwright sẽ đợi trang web tải. Nếu quá thời gian này trang chưa xong, nó sẽ báo lỗi (Crash). Mặc định: 30,000 ms (30 giây).
- referer: Giả lập rằng bạn đến từ một trang web khác (ví dụ: giả vờ như bạn bấm vào link này từ Google).Ứng dụng: Vượt qua một số hệ thống chống cào dữ liệu (Anti-crawl).
```
**Ex**
```python
import asyncio
from playwright.async_api import async_playwright

async def main():
    async with async_playwright() as p:
        browser = await p.chromium.launch(headless=False)
        page = await browser.new_page()

        # SỬ DỤNG GOTO VỚI CÁC THAM SỐ
        await page.goto(
            "https://batdongsan.com.vn", 
            wait_until="networkidle", # Đợi cho đến khi mạng "rảnh", dữ liệu tải hết
            timeout=10000,            # Chỉ đợi tối đa 10 giây, quá 10s là bỏ qua
            referer="https://www.google.com" # Giả vờ đến từ Google
        )

        print("Trang web đã tải xong hoàn toàn!")
        await browser.close()

asyncio.run(main())
```


**Ex**
```python
from playwright.async_api import Playwright, BrowserContext

async def create_browser_context(
    p: Playwright,
    profile_dir: str = '/home/thang/pw-chrome-profile',
    headless: bool = False
 ) -> BrowserContext:
    return await p.chromium.launch_persistent_context(
        user_data_dir=profile_dir,
        headless=False,
        args=[
            "--disable-blink-features=AutomationControlled",
            "--disable-images",
            "--disable-css",
            "--start-maximized"
        ]
    )
```