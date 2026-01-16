- [root - Bản đồ nhanh (đọc trước)](#root---bản-đồ-nhanh-đọc-trước)
- [apps/](#apps)
  - [frappe/](#frappe)
  - [my-app/](#my-app)
    - [my-app/](#my-app-1)
- [config/ – HẬU TRƯỜNG (SERVICE)](#config--hậu-trường-service)
- [logs/ – HỘP ĐEN](#logs--hộp-đen)
- [Procfile – KỊCH BẢN CHẠY](#procfile--kịch-bản-chạy)
- [patches.txt – LỊCH SỬ CẬP NHẬT](#patchestxt--lịch-sử-cập-nhật)

---

# root - Bản đồ nhanh (đọc trước)
```bash
frappe-bench/
├── apps        → CODE (logic)
├── sites       → DATA (dữ liệu + cấu hình site)
├── env         → PYTHON (môi trường)
├── config      → SERVICE (redis, process)
├── logs        → LOG (nhật ký)
├── scripts
├── patches.txt
├── procfile
```

# apps/
```bash
Não bộ (code). Toàn bộ source code của framework Frappe nằm ở đây
- Backend Python
- API
- ORM
- Permission
- Workflow
- UI core
```
**tree**
```bash
apps/
└── frappe/
└── my_custom_hr_app    → App mới do dev tự cài vào

- Không sửa code trong frappe trừ khi bạn biết rõ
```

## frappe/
```bash
- Đây là Frappe Framework source code gốc.
- Nó chứa:
    + ORM
    + Doctype engine
    + Permission
    + API
    + UI backend
    + Toàn bộ xương sống của frappe
- frappe = 1 app nhưng là app nền tảng.
# sites/
Dữ liệu + cấu hình.
```bash
sites/
├── apps.json                   → Danh sách app được enable. Frappe đọc file này để biết: site này dùng app nào. Thiếu → site không 
                                  load app
├── apps.txt                      
├── assets/                     → File tĩnh đã build: JS, CSS, Image. Được sinh ra từ: bench build. Không chỉnh tay
├── dev.local                   
└── common_site_config.json     → Cấu hình dùng chung cho tất cả site Ví dụ: DB host, Redis URL, Socket IO, Background worker. Khi 
                                  Frappe start → đọc file này đầu tiên

- Đây là nơi Frappe sống thực sự
```

## my-app/
```bash
my-app/
├── .git/                   → Quản lý source code (lưu lịch sử commit, branch, diff) → không xóa
├── .gitinore               → Nói với git không track, rất quan trọng khi làm team                      
├── READ.md                 → Mô tả app làm cái gì, cách cài, cách chạy -> không ảnh hưởng runtime, nên viết cho team tương lại
├── license.txt             → bản quyền, bắt buộc nếu open-source    
├── .eslintrc               → check js, chỉ dùng khi bạn viết JS/Frontend              
└── editorconfig            → chuẩn format code, không ảnh hưởng khi chạy, chỉ ảnh hưởng cách viết code
```
### my-app/
```bash
- DocType = bản thiết kế (form + dữ liệu + luật) cho 1 loại giấy tờ.
- Ví dụ đời thực (rất quan trọng): Một tờ “Đơn xin nghỉ phép”
    + Luôn có: Tên người xin, Ngày nghỉ, Lý do, Trạng thái (chờ duyệt / đã duyệt)
    + Trong Frappe: Đơn xin nghỉ phép = 1 DocType. Mỗi lần bạn tạo đơn → đó là 1 Document
```
**Ex**
```bash
DocType: Leave Application
Document: Đơn xin nghỉ của Thắng ngày 10/1
```
**Bên trong 1 DocType có những gì?**
```bash
1. Fields (Trường): Ví dụ: Tên bài viết
    - Ảnh
    - Tác giả
    - Trạng thái
    - Giống cột trong bảng DB
2. Giao diện (UI)
    - List để xem
    - Search, filter
    - Không cần code
    - Form để nhập
3. Quyền (Permission)
    - Ai được xem?
    - Ai được tạo?
    - Ai được xóa?
    -> Không phải viết middleware
4. Hành vi (Behavior)
    - Khi bấm Save → kiểm tra gì?
    - Khi Submit → làm gì?
```

# config/ – HẬU TRƯỜNG (SERVICE)
```bash
config/
├── redis_cache.conf
├── redis_queue.conf
├── pids/
├── ...

- Cấu hình service chạy nền
- Bench dùng để:
    + khởi động
    + quản lý
    + stop service
- Không sửa nếu chưa hiểu
```

# logs/ – HỘP ĐEN
```bash
logs/
└── bench.log

- Nơi debug
    + Frappe lỗi → vào đây
    + Bench không start → vào đây
    + 80% debug nhìn file này
```

# Procfile – KỊCH BẢN CHẠY
Nói cho Bench biết phải chạy những gì.
**Ex**
```bash
web
worker
scheduler

- Bench đọc file này khi start
```

# patches.txt – LỊCH SỬ CẬP NHẬT
```bash
- Ghi lại:
    + migration
    + patch DB
-Không sửa tay
``