# page.mouse.wheel()
```bash
- page.mouse.wheel(dx, dy) dùng để giả lập thao tác lăn chuột (scroll) trên trang web.
- Thường dùng khi:
    + Trang không scroll được bằng page.evaluate
    + Test lazy loading, infinite scroll
    + Giả lập hành vi người dùng thật
```
**Syn**
```bash
await page.mouse.wheel(deltaX, deltaY)

- deltaX	: Scroll ngang (trái/phải)
- deltaY	: Scroll dọc (lên/xuống)
- Giá trị dương = scroll xuống / sang phải
- Giá trị âm = scroll lên / sang trái
```
3️⃣ Demo cơ bản – scroll xuống trang
import { chromium } from '@playwright/test';

const browser = await chromium.launch();
const page = await browser.newPage();

await page.goto('https://example.com');

// Scroll xuống 500px
await page.mouse.wheel(0, 500);

await browser.close();

4️⃣ Scroll nhiều lần (mô phỏng người dùng)
for (let i = 0; i < 5; i++) {
  await page.mouse.wheel(0, 300);
  await page.waitForTimeout(500); // đợi load nội dung
}


➡️ Rất hay dùng cho infinite scroll

5️⃣ Scroll lên
await page.mouse.wheel(0, -400);

6️⃣ Scroll ngang (carousel, bảng rộng)
await page.mouse.wheel(300, 0);

7️⃣ Scroll tại vị trí cụ thể (quan trọng ⚠️)

mouse.wheel scroll tại vị trí con trỏ chuột, vì vậy nên move chuột trước

// Di chuyển chuột vào giữa màn hình
await page.mouse.move(500, 400);

// Scroll
await page.mouse.wheel(0, 600);

8️⃣ Demo scroll đến khi load xong (infinite scroll)
let previousHeight = 0;

while (true) {
  const currentHeight = await page.evaluate(() => document.body.scrollHeight);
  if (currentHeight === previousHeight) break;

  previousHeight = currentHeight;
  await page.mouse.wheel(0, 1000);
  await page.waitForTimeout(1000);
}

9️⃣ So sánh với cách scroll khác
Cách	Khi nào dùng
page.mouse.wheel	Mô phỏng người dùng thật
page.evaluate(() => window.scrollTo())	Scroll nhanh, đơn giản
locator.scrollIntoViewIfNeeded()	Scroll tới element cụ thể

Ví dụ scroll tới element (khuyên dùng nếu có selector):

await page.locator('#footer').scrollIntoViewIfNeeded();

10️⃣ Lỗi thường gặp ❌
❌ Scroll nhưng trang không di chuyển

➡️ Do chuột chưa nằm trong vùng scroll

✅ Fix:

await page.mouse.move(100, 100);
await page.mouse.wheel(0, 500);


Nếu bạn đang:

Test React / Vue infinite scroll

Scroll trong modal / div có overflow

Dùng Playwright Test (test() syntax)

👉 gửi mình case cụ thể, mình viết demo đúng chuẩn cho bạn nhé 🚀

import asyncio
from playwright.async_api import async_playwright

async def main():
    async with async_playwright() as p:
        context = await p.chromium.launch_persistent_context(
            user_data_dir="/home/thang/pw-chrome-profile",
            headless=False,
            args=[
                "--disable-blink-features=AutomationControlled",

                # 🔥 Màn desktop 1360x768 ở PHÍA TRÊN
                "--window-size=1360,768",
                # "--window-position=0,-768"
            ],
            viewport=None
        )

        page = await context.new_page()
        await page.goto("https://www.youtube.com/", timeout=60000)

        # Chuột giữa màn desktop
        await page.mouse.move(680, 384)

        # Scroll chậm, thấy rõ
        for _ in range(25):
            await page.mouse.wheel(0, 80)
            await page.wait_for_timeout(200)

        await page.wait_for_timeout(5000)
        await context.close()

asyncio.run(main())
