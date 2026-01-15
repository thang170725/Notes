```bash
viết class trực tiếp trong HTML thay vì viết CSS riêng.
```
**Ex**
```html
<button class="bg-blue-500 text-white px-4 py-2 rounded">
  Click me
</button>
```
```js
<script src="https://cdn.tailwindcss.com"></script>
```

# Màu sác: bg- & text-

# Khoảng cách: p-, m-

# Kích thước: w-, h-

# Bo góc: rounded

# Bóng: shadow

📌 Mục tiêu: nhìn class là hiểu giao diện

🔹 BƯỚC 2: Layout (quan trọng nhất)

Học kỹ:

Flexbox:
flex, items-center, justify-between

Grid:
grid, grid-cols-3, gap-4

Ví dụ:

<div class="flex items-center justify-between">
  <div>Logo</div>
  <div>Menu</div>
</div>

🔹 BƯỚC 3: Responsive (Tailwind rất mạnh phần này)

Học:

sm:

md:

lg:

xl:

Ví dụ:

<div class="text-sm md:text-lg lg:text-xl">
  Responsive text
</div>

🔹 BƯỚC 4: Component cơ bản

Tự làm:

Button

Card

Navbar

Form đăng nhập

👉 Đây là lúc bạn nhớ Tailwind rất nhanh

🔹 BƯỚC 5: Cài Tailwind chuẩn (khi đã quen)

Dùng:

Node.js

Tailwind CLI hoặc Vite

Dành cho khi:

Làm project thật

Dùng React / Vue / Next.js

4️⃣ Tài liệu & nguồn học tốt (miễn phí)
📘 Tài liệu chính thức (rất dễ đọc)

👉 https://tailwindcss.com/docs

🎥 Video (YouTube)

Tìm:

Tailwind CSS crash course

Tailwind CSS for beginners

(Kênh hay: Traversy Media, Net Ninja)

5️⃣ Cách học nhanh nhất (kinh nghiệm thực tế)

✅ Đừng học thuộc class
✅ Copy ví dụ → sửa lại
✅ Làm giao diện thật (login, dashboard, landing page)

6️⃣ Gợi ý lộ trình 7 ngày

Ngày 1: Màu, spacing, text

Ngày 2: Flexbox

Ngày 3: Grid

Ngày 4: Responsive

Ngày 5: Button + Card

Ngày 6: Navbar + Form

Ngày 7: Clone 1 giao diện đơn giản