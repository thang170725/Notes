- [Bản đồ nhanh](#bản-đồ-nhanh)
- [site\_config.json – NÃO CỦA SITE (QUAN TRỌNG NHẤT)](#site_configjson--não-của-site-quan-trọng-nhất)
- [private/ – KHO KÍN (USER KHÔNG XEM ĐƯỢC)](#private--kho-kín-user-không-xem-được)
- [public/ – KHO MỞ (AI CŨNG XEM ĐƯỢC 😄)](#public--kho-mở-ai-cũng-xem-được-)
- [Ví dụ về site](#ví-dụ-về-site)

---

```text
- Thư mục site = “nhà riêng” của 1 hệ thống Frappe
- Mỗi site:
    + có DB riêng
    + có log riêng
    + có file riêng
    + có config riêng
```

# Bản đồ nhanh
```bash
dev.local/
├── site_config.json   → NÃO (cấu hình)
├── private/           → KHO KÍN
├── public/            → KHO MỞ
├── logs/              → NHẬT KÝ
├── locks/             → KHÓA CỬA
```

# site_config.json – NÃO CỦA SITE (QUAN TRỌNG NHẤT)
```bash
{
  "db_name": "_a1b2c3",
  "db_password": "******",
  "db_type": "mariadb"
}

Chứa:
- tên database
- mật khẩu DB
- redis
- socket
- secret key
- Khi Frappe nhận request:
URL → xác định site → đọc site_config.json → connect DB
KHÔNG commit file này lên Git
```

# private/ – KHO KÍN (USER KHÔNG XEM ĐƯỢC)
```bash
private/
├── backups
└── files
```
**private/backups**
```text
- Nơi Frappe:
  + ump DB
  + backup file
  + Lệnh: bench --site dev.local backup
```
**private/files**
File upload KHÔNG public
  + hợp đồng
  + CMND
  + file nhạy cảm
Không truy cập bằng URL

# public/ – KHO MỞ (AI CŨNG XEM ĐƯỢC 😄)
```bash
public/
└── files

File upload công khai
- ảnh
- brochure
- tài liệu marketing
- Truy cập qua: https://dev.local/files/abc.png
```

4️⃣ logs/ – NHẬT KÝ RIÊNG CỦA SITE
logs/
├── database.log
└── database.log.1


👉 Log liên quan:

DB query

lỗi migration

lỗi permission

📌 Debug lỗi site → vào đây

5️⃣ locks/ – Ổ KHÓA (CHỐNG LOẠN)
locks/
└── bench_new_site.lock


👉 Dùng để:

tránh 2 process đụng nhau

tránh chạy migration trùng

📌 Bạn KHÔNG BAO GIỜ đụng vào

6️⃣ Cái gì KHÔNG thấy nhưng RẤT quan trọng?

👉 Database

DB không nằm trong thư mục

nhưng site_config.json trỏ tới DB

📌 Xóa thư mục site ≠ xóa DB (trừ khi bench làm)

# Ví dụ về site
2️⃣ Sites (mỗi site = 1 instance)

Giả sử bạn có 3 khách hàng:

Site	DB	Mục đích
acme.taskmgmt.local	db_acme	Công ty ACME dùng để quản lý công việc thực tế
beta.taskmgmt.local	db_beta	Công ty Beta dùng để test / thử nghiệm
dev.taskmgmt.local	db_dev	Dùng để phát triển, thử feature mới

Sơ đồ:

task_mgmt_bench/
 ├── apps/
 └── sites/
     ├── acme.taskmgmt.local  -> db_acme
     ├── beta.taskmgmt.local  -> db_beta
     └── dev.taskmgmt.local   -> db_dev

3️⃣ Tại sao mỗi site cần DB riêng

ACME có dữ liệu thật của nhân viên, project, task → phải cách ly

Beta chỉ để test → dữ liệu khác

Dev để lập trình → dữ liệu fake, không ảnh hưởng production

Nếu tất cả dùng chung 1 DB thì:

Dữ liệu test và production lẫn lộn → dễ phá hỏng dữ liệu thật

Không thể rollback hoặc restore riêng từng môi trường

4️⃣ Ví dụ chi tiết về workflow

Dev team thêm 1 feature “Giao task tự động cho team member”.

Feature deploy trên dev.taskmgmt.local → dữ liệu dev riêng

QA test trên beta.taskmgmt.local → dữ liệu test riêng

Sau khi ok → deploy cho acme.taskmgmt.local → dữ liệu production an toàn

5️⃣ Tóm tắt
Khái niệm	Trong dự án quản lý công việc
Bench	task_mgmt_bench chứa code chung
Apps	tasks_app, users_app, notifications_app
Site	acme.taskmgmt.local, beta.taskmgmt.local, dev.taskmgmt.local
DB	db_acme, db_beta, db_dev

✅ Kết luận: Bench = code, Site = instance + DB