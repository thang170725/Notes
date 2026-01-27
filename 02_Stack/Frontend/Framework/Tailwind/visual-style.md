```bash
- Để Thiết kế hình dạng đẹp cho box (radius, image, shadow, ...)
```
---
- [rounded](#rounded)
- [shadow](#shadow)
---

# rounded
```bash
- Bo góc cho phần tử.
```
**Syn**
```bash
- rounded-sm	: bo nhẹ
- rounded	    : bo vừa
- rounded-md	: bo trung bình
- rounded-lg	: bo khá lớn
- rounded-xl	: bo rất lớn
- rounded-full	: bo tròn hoàn toàn
- rounded-tl-lg : bo 1 góc trên trái
- rounded-bl-lg : bo 1 góc dưới trái

**Ex**
```js
<div class="w-40 h-20 bg-blue-500 rounded-lg"></div>
```

# shadow
```bash
- Đổ bóng lớn (large shadow) cho phần tử.
- Dùng để tạo cảm giác nổi lên khỏi nền.
```
**Syn**
```bash
- shadow-sm	    : bóng rất nhẹ
- shadow	    : bóng mặc định
- shadow-md	    : bóng vừa
- shadow-lg	    : bóng rõ, sâu
- shadow-xl	    : bóng rất sâu
- shadow-2xl	: bóng cực sâu
```
**Ex**
```js
<div class="w-40 h-20 bg-white shadow-lg"></div>

Trông giống card nổi.
```
# Chỉnh độ dày chữ
**Ex**
```js
<p className="font-thin">Thin (100)</p>
<p className="font-light">Light (300)</p>
<p className="font-normal">Normal (400)</p>
<p className="font-medium">Medium (500)</p>
<p className="font-semibold">Semi Bold (600)</p>
<p className="font-bold">Bold (700)</p>
<p className="font-extrabold">Extra Bold (800)</p>
<p className="font-black">Black (900)</p>
```

📌 Hay dùng nhất trong UI

Text thường: font-normal, font-medium

Menu / button: font-medium, font-semibold

Title: font-bold

🎯 Hover đổi độ dày
<li className="font-medium hover:font-semibold transition-all duration-300">
  Dashboard
</li>

🧠 Font + size + màu (combo thực tế)
<h1 className="text-xl font-semibold text-white">
  Smart Recipe
</h1>

❌ Lỗi hay gặp
font-600      // ❌ không tồn tại
font-bold-2   // ❌ không có

🧪 Kiểm tra font bạn dùng có hỗ trợ weight không

⚠️ Nếu font KHÔNG hỗ trợ nhiều weight (ví dụ font custom):

Dùng font-bold cũng không dày hơn

Đây là lỗi font, không phải Tailwind

🔧 Nếu bạn muốn weight tuỳ chỉnh (nâng cao)
// tailwind.config.js
extend: {
  fontWeight: {
    extra: 950,
  }
}

<p className="font-extra">Extra heavy</p>

🔥 Ví dụ cho sidebar menu
<Link
  to="/dashboard"
  className="block p-2 font-medium text-white hover:font-semibold transition-all duration-300"
>
  Dashboard
</Link>


Nếu bạn muốn:

text đậm dần khi hover

title + subtitle chuẩn layout

dùng font Google / font local
border trong Tailwind
✅ Border cơ bản
<div className="border">...</div>


👉 mặc định: 1px solid #e5e7eb

🎨 Border màu
border-red-500
border-slate-300
border-[#ff5733]

📏 Border độ dày
border       // 1px
border-2     // 2px
border-4     // 4px
border-8     // 8px

📐 Border theo từng cạnh
border-t
border-b
border-l
border-r

🔵 Border bo góc
rounded
rounded-md
rounded-lg
rounded-full

✨ Border style
border-dashed
border-dotted
border-double

🔥 Ví dụ
<div className="border border-slate-300 rounded-md p-4">
  Card
</div>