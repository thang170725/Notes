# page.goto(url)
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