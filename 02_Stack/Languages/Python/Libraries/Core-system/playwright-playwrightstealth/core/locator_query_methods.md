- [page.locator() \& locator.click() \& locator.fill() \& locator.count()](#pagelocator--locatorclick--locatorfill--locatorcount)
  - [search google](#search-google)

---

```text
- NHÓM LOCATOR – CHUẨN PLAYWRIGHT MỚI. RẤT QUAN TRỌNG – nên dùng thay selector cũ.
- Vì sao locator tốt hơn?
  + Tự wait
  + Ít lỗi
  + Code rõ ràng
```

# page.locator() & locator.click() & locator.fill()
## search google
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()

    page.goto("https://www.google.com")

    # Tạo locator
    search_box = page.locator("textarea[name='q']")

    # Chờ locator sẵn sàng
    search_box.wait_for()

    # Gõ chữ
    search_box.fill("locator playwright python")

    # Enter
    search_box.press("Enter")

    page.wait_for_timeout(5000)
    browser.close()
```
**Ex2**
```python
from playwright.sync_api import sync_playwright
import random
import time

with sync_playwright() as p:
    browser = p.chromium.launch(
        headless=False,
        slow_mo=50  # làm chậm hành động
    )

    context = browser.new_context(
        user_agent=(
            "Mozilla/5.0 (X11; Linux x86_64) "
            "AppleWebKit/537.36 (KHTML, like Gecko) "
            "Chrome/120.0.0.0 Safari/537.36"
        ),
        viewport={"width": 1366, "height": 768},
        locale="vi-VN"
    )

    page = context.new_page()

    # 🔥 Xóa dấu hiệu webdriver
    page.add_init_script("""
        Object.defineProperty(navigator, 'webdriver', {
            get: () => undefined
        });
    """)

    # Vào Google
    page.goto("https://www.google.com", wait_until="domcontentloaded")

    # Nghỉ như người suy nghĩ
    time.sleep(random.uniform(2, 4))

    search_box = page.locator("textarea[name='q']")
    search_box.wait_for()

    # Gõ từng chữ (giống người)
    search_box.click()
    for char in "playwright python tutorial":
        search_box.type(char)
        time.sleep(random.uniform(0.05, 0.2))

    search_box.press("Enter")

    page.wait_for_timeout(5000)
    browser.close()
```

from playwright.sync_api import sync_playwright

USER_DATA_DIR = "/home/thang/pw-firefox-profile"

with sync_playwright() as p:
    context = p.firefox.launch_persistent_context(
        user_data_dir=USER_DATA_DIR,
        headless=False,
        viewport={"width": 1280, "height": 800}
    )

    page = context.pages[0] if context.pages else context.new_page()
    page.goto("https://www.youtube.com", wait_until="domcontentloaded")

    search_box = page.locator("input[name='search_query']:not([hidden])")
    search_box.wait_for(state="visible", timeout=30000)

    search_box.fill("locator playwright python")
    search_box.press("Enter")

    page.wait_for_timeout(5000)

    print("👉 Login xong rồi quay lại terminal nhấn Enter")
    input()

    context.close()

from playwright.sync_api import sync_playwright
import time
import random


def human_type(page, locator, text):
    locator.click()
    time.sleep(0.5)
    for ch in text:
        page.keyboard.type(ch)
        time.sleep(random.uniform(0.12, 0.22))


def human_scroll(page):
    page.mouse.wheel(0, random.randint(700, 1000))
    time.sleep(random.uniform(1.0, 1.6))


def skip_ads_if_any(page):
    try:
        skip_btn = page.locator(
            "button.ytp-ad-skip-button, button:has-text('Skip')"
        )
        skip_btn.wait_for(timeout=15000)
        skip_btn.click()
        print("⏭ Đã skip quảng cáo")
    except:
        print("ℹ️ Không có quảng cáo")


with sync_playwright() as p:
    context = p.chromium.launch_persistent_context(
        user_data_dir="/home/thang/pw-chrome-profile",
        headless=False
    )

    page = context.pages[0]

    # 1️⃣ Mở YouTube
    page.goto("https://www.youtube.com", wait_until="domcontentloaded")
    page.wait_for_load_state("networkidle")
    print("🌐 Đã mở YouTube")

    # 2️⃣ Search
    search_box = page.locator('input[name="search_query"]')
    print("⏳ Đợi search box...")
    search_box.wait_for(state="visible", timeout=60000)

    human_type(page, search_box, "list edm hot doyin")
    print("🔎 Đã gõ xong")
    search_box.press("Enter")

    # 3️⃣ Đợi trang kết quả
    page.wait_for_load_state("networkidle")
    time.sleep(2)

    # 4️⃣ Scroll cho đến khi có đủ 10 video THẬT
    videos = page.locator("ytd-video-renderer")
    round_scroll = 0

    while videos.count() < 10:
        human_scroll(page)
        round_scroll += 1
        print(f"🔄 Scroll {round_scroll}, video hiện có: {videos.count()}")

        if round_scroll > 12:
            raise Exception("❌ Không tìm đủ 10 video")

    print("✅ Đã đủ video")

    # 5️⃣ CLICK VIDEO THỨ 10 (CLICK LINK THẬT)
    video_10 = videos.nth(9)
    video_link = video_10.locator("a#thumbnail")

    video_link.scroll_into_view_if_needed()
    time.sleep(1)

    video_link.click()
    print("▶️ Đã click video thứ 10")

    # 6️⃣ ĐỢI VÀO TRANG /watch
    page.wait_for_url("**/watch**", timeout=30000)
    print("🎬 Đã vào trang xem video")

    # 7️⃣ ĐỢI VIDEO ELEMENT THẬT
    video_tag = page.locator("video.html5-main-video")
    video_tag.wait_for(state="visible", timeout=30000)
    print("🎵 Video đang phát")

    time.sleep(3)

    # 8️⃣ Skip quảng cáo nếu có
    skip_ads_if_any(page)

    input("⏸ Đang phát nhạc, nhấn Enter để thoát")
    context.close()
