- [Tạo project \& môi trường ảo python (thư mục làm việc)](#tạo-project--môi-trường-ảo-python-thư-mục-làm-việc)
- [Cập nhật và cài đặt gói hệ thống cốt lõi](#cập-nhật-và-cài-đặt-gói-hệ-thống-cốt-lõi)
- [Thiết lập liên kết python](#thiết-lập-liên-kết-python)
- [Cài đặt MariaDB và cấu hình frappe \& khởi động lại mariadb](#cài-đặt-mariadb-và-cấu-hình-frappe--khởi-động-lại-mariadb)
- [Cài đặt node.js và yarn](#cài-đặt-nodejs-và-yarn)
- [Cài đặt Frappe Bench CLI](#cài-đặt-frappe-bench-cli)
- [Tạo thư mục cha](#tạo-thư-mục-cha)
- [Khởi tạo bench.](#khởi-tạo-bench)
- [Tạo site mới](#tạo-site-mới)
- [Sửa file hosts](#sửa-file-hosts)
- [Chạy frappe bench](#chạy-frappe-bench)
- [Tạo App (mã nguồn)](#tạo-app-mã-nguồn)
- [Cài app vào site](#cài-app-vào-site)
- [Build Assets và đồng bộ database](#build-assets-và-đồng-bộ-database)
- [Kích hoạt developer mode](#kích-hoạt-developer-mode)
- [Cài Vue](#cài-vue)
- [Vào site\_config ở site](#vào-site_config-ở-site)
- [Cách 2](#cách-2)

---

# Tạo project & môi trường ảo python (thư mục làm việc)
```bash
1. mkdir ~/frappe-vue-test
2. cd ~/frappe-vue-test
3. python3.10 -m venv .venv  : Tạo virtual environment với Python 3.10
4. source .venv/bin/activate
```
**Kiểm tra**
```bash
which python
python --version
pip --version
```

# Cập nhật và cài đặt gói hệ thống cốt lõi
```bash
sudo apt update             : cập nhật danh sách phần mềm.
sudo apt install -y         : cài hàng loạt phần mềm 1 lần
    git \                   : dùng để tải source code, frappe được clone từ gitHub
    build-essential \       : bộ công cụ biên dịch C/C++
    curl \                  : tải file từ internet bằng dòng lệnh. Frappe / Bench dùng curl để: tải script, tải Node, tải tool phụ
    python3-dev \           : Cho phép Python build thư viện “có lõi C”
    python3-pip \           : Trình cài thư viện Python
    python3-venv \          : Tạo môi trường ảo
    redis-server \          : Bộ nhớ nhanh (cache + queue). Frappe dùng Redis cho: cache background job, task async
                              Ví dụ: gửi email, xử lý dữ liệu nền, crawl / sync. Không có Redis → Frappe không khởi động
    libmariadb-dev \        : Thư viện cho Python nói chuyện với MariaDB, Khi bạn cài: pip install mysqlclient Nó cần: header 
                              file lib mariadb. Thiếu → không kết nối DB được
    mariadb-server \        : Database server
    mariadb-client \        : Tool kết nối & quản lý DB
    pkg-config              : Trợ lý cho compiler. Nó giúp: tìm thư viện hệ thống, tìm đúng version, link đúng file Không dùng trực 
                              tiếp, nhưng: thiếu → build lib dễ fail
sudo apt update
sudo apt install -y \
    git \
    build-essential \
    curl \
    python3-dev \
    python3-pip \
    python3-venv \
    redis-server \
    libmariadb-dev \
    mariadb-server \
    mariadb-client \
    pkg-config

```

# Thiết lập liên kết python
```bash
# Gói này sẽ giúp lệnh 'python' gọi đến 'python3'
sudo apt install -y python-is-python3
```

# Cài đặt MariaDB và cấu hình frappe & khởi động lại mariadb
```bash
sudo systemctl start mariadb    : bật MariaDB lên để nó chạy
sudo mysql_secure_installation  : khóa & dọn dẹp MariaDB cho an toàn
```
**Kiểm tra nhanh DB có chạy không**
```bash
systemctl status mariadb
```
**tùy chọn**
```text
Cấu hình MariaDB cho Frappe: Mở file cấu hình database (thường là /etc/mysql/mariadb.conf.d/50-server.cnf) và thêm/chỉnh sửa các cài đặt sau vào phần [mysqld] để đảm bảo hỗ trợ UTF-8mb4 và chế độ nghiêm ngặt:
```
```bash
Ini, TOML
[mysqld]
# Thiết lập bộ ký tự
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci

# Thiết lập chế độ nghiêm ngặt (Strict Mode)
sql-mode="STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"

[mysql]
default-character-set = utf8mb4

```
**Cuối cùng**

```bash
sudo systemctl restart mariadb  : Khởi động lại MariaDB
```

# Cài đặt node.js và yarn
```bash
curl -sL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
sudo npm install -g yarn
```

# Cài đặt Frappe Bench CLI
```bash
pip3 install frappe-bench
```

# Tạo thư mục cha
```bash
mkdir fw
cd fw
```

# Khởi tạo bench. 
Lệnh này sẽ tải Frappe Framework về và tạo thư mục 'frappe-bench'
```bash
bench init frappe-bench \
  --frappe-branch version-15 \
  --python /usr/bin/python3.11
cd frappe-bench
```

# Tạo site mới
```bash
bench new-site dev.local
```
**Tại sao phải tạo site mới**
```text
- Site = 1 hệ thống độc lập hoàn chỉnh. Không có site → Frappe không chạy được. Bạn KHÔNG thao tác trực tiếp trên Frappe core.
- Ví dụ đời thường (quan trọng nhất) Frappe giống gì?
    + Frappe = Windows / Android
    + Site = từng máy tính / từng điện thoại
    + Bạn không: mở Windows rồi lưu dữ liệu chung cho tất cả máy mà mỗi máy có user, app, dữ liệu riêng
- Nếu không có site thì chuyện gì xảy ra? Giả sử KHÔNG có site:
    + User A
    + User B
    + Công ty X
    + Công ty Y
    -> Tất cả: chung DB, chung config, chung quyền -> toang toàn bộ
- Site thực chất chứa những gì? Mỗi site có:
    + 1 database riêng
    + user riêng
    + quyền riêng
    + config riêng
    + dữ liệu riêng Nằm ở: sites/dev.local/
```
**Vì sao Frappe bắt buộc phải có site?**
```text
- Vì Frappe: là framework đa tenant
- thiết kế để:
    + 1 code
    + nhiều hệ thống
- Không tạo site thì:
    + không có DB
    + không có user
    + không có config
    + không có dữ liệu
```
**Ví dụ**
```text
- Bạn làm dự án BĐS + AI. Bạn muốn:
    + dev thử nghiệm
    + test crawl
    + prod chạy thật
- Bạn tạo:
    + dev.local
    + test.local
    + prod.domain.com
    + Mỗi site:
        + DB riêng
        + data riêng
        + không đụng nhau
```

# Sửa file hosts
```bash
sudo nano /etc/hosts
di chuyển con trỏ xuống cuối
gõ: 127.0.0.1   dev.local
Bấm theo đúng thứ tự:
1. CTRL + S
3. CTRL + X (Exit)
-> Xong, nano sẽ tự thoát.
```
Hoặc
```bash
bench --site dev.local add-to-hosts
```
**Kiểm tra**
```bash
ping dev.local
nếu thây: PING dev.local (127.0.0.1) -> OK
```

# Chạy frappe bench
```bash
cd ~/workspace/thang-dev/fw/frappe-bench
bench start
Mở trình duyệt: http://dev.local:8000 hoặc http://dev.local:8000/desk
```
**Login**
```bash
Username: Administrator
Password: (mật khẩu bạn nhập lúc tạo site)
```
**Quên mật khẩu**
```bash
bench --site dev.local set-admin-password
```

# Tạo App (mã nguồn)
**Điều kiện**
```bash
cd ~/workspace/thang-dev/fw/frappe-bench
ls
Phải thấy: apps  sites  env  Procfile ...
```
**Chạy lệnh tạo app**
```bash
bench new-app my_custom_hr_app
```

# Cài app vào site
Tạo app xong chưa chạy được. Phải gắn nó vào site dev.local
```bash
bench --site dev.local install-app my_custom_hr_app
```
**Kiểm tra**
```bash
bench --site dev.local list-apps hoặc Mở giao diện: Settings → Apps
```

# Build Assets và đồng bộ database
```bash
bench build
bench --site dev.local migrate
bench start
```

# Kích hoạt developer mode
```text
- Developer Mode = chế độ dành cho người làm ứng dụng, không phải người chỉ sử dụng hệ thống.
- Khi bật Developer Mode, Frappe coi mọi thứ bạn tạo (DocType, Report, Web Form,…) là MÃ NGUỒN, chứ không chỉ là dữ liệu trong database.
- Nhờ đó:
    + Có file .json, .py, .js thật sự
    + Có thể dùng Git
    + Có thể deploy, backup, code review
    + Có thể viết logic tùy biến
```
**Không bật Developer Mode thì chuyện gì xảy ra?**
**Giả sử KHÔNG bật developer_mode mà bạn tạo DocType Article**
```text
- Điều xảy ra:
  + DocType chỉ được lưu trong database
  + KHÔNG có file article.json, article.py, article.js
  + Git không biết gì để commit
  + Sang server khác → mất DocType
  + Không viết được logic backend/frontend chuẩn chỉnh
- Trường hợp này phù hợp cho:
  + Người dùng cuối
  + Admin chỉ cấu hình ERP
  + KHÔNG phù hợp cho dev
```
**Vì sao Frappe “ép” bật Developer Mode khi làm app?**
- Frappe được thiết kế theo triết lý:
  + Everything is Metadata + Code
DocType không chỉ là bảng DB, mà là:
  + Model
  + View
  + Controller
  + Permission
  + Workflow
  + Validation
- Nên Frappe cần export định nghĩa DocType ra file để:
  + Theo dõi thay đổi
  + Đồng bộ giữa các site
  + Deploy CI/CD
  + Rollback khi lỗi
  + Tất cả việc đó chỉ làm được khi bật Developer Mode.
**Developer Mode đã làm gì “dưới mui xe”?**
```text
- Khi bạn bật:
  + bench set-config -g developer_mode true
- Frappe thay đổi hành vi như sau:
  + Trước (developer_mode = false)
  + DocType → DB
  + Custom Field → DB
  + Script → DB
  + Sau (developer_mode = true)
  + DocType → article.json
  + Logic server → article.py
  + Logic client → article.js
  + Test → test_article.py
DB chỉ là runtime, còn source of truth là code.
```

```bash
bench set-config -g developer_mode true
```

# Cài Vue
```bash
cd apps/todo
npx degit netchampfaris/frappe-ui-starter frontend
cd frontend
yarn
yarn dev
```

# Vào site_config ở site
paste nội dung này vào.
```bash
"allow_cors": "*",
 "ignore_csrf": 1
```

# Cách 2
```bash
1. mkdir dev & cd dev
2. python3.12 -m venv .venv
3. source .venv/bin/activate
4. bench init frappe-bench-15 --frappe-branch version-15 --python /usr/bin/python3.12
5. cd frappe-bench-15/
6. bench new-site mbw15.ts
7. bench use mbw15.ts
8. bench set-config -g developer_mode 1
9. bench get-app erpnext https://github.com/frappe/erpnext --branch version-15
10. bench install-app erpnext
11. bench start (lỗi)
```