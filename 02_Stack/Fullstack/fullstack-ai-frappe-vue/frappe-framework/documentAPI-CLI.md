- [vào site cụ thể](#vào-site-cụ-thể)
- [exit()](#exit)
- [.new\_doc() \& .title](#new_doc--title)
- [update data](#update-data)
- [.get\_last\_doc()](#get_last_doc)
- [get\_all](#get_all)
- [get\_list](#get_list)
- [delete\_doc()](#delete_doc)
- [Commit()](#commit)
- [Rollback()](#rollback)
- [.as\_dict()](#as_dict)
- [.get\_meta \& .fields](#get_meta--fields)
  - [.has\_field()](#has_field)

---

# vào site cụ thể
```bash
bench --site dev.local console
```

# exit()
Thoát.

# .new_doc() & .title
```bash
doc = frappe.new_doc('')
Cách tạo ra một doctype mới.

# frappe.get_doc() & .insert() & .save()
Tạo document hoặc lấy document theo name.
**Ex: Tạo document**
```bash
doc = frappe.get_doc({
    "doctype": "Article",
    "article_name": "Clean Code",
    "isbn": "1234567890",
    "status": "Available"
})
doc.insert()
```
**Ex: Lấy document theo name**
```bash
doc = frappe.get_doc("Article", "My First Book")
- Lấy một document article có name="My First Book"" từ database.
```
# update data
Thay đổi dữ liệu.
**Ex**
```bash
doc.status = "Issued" // status là tên cột của bảng
doc.save()
```

3️⃣ Query dữ liệu (rất hay dùng)
🔹 frappe.db.exists
frappe.db.exists("Article", "Clean Code")

# .get_last_doc()
```bash
doc = frappe.get_last_doc(
    doctype, 
    filters={'status': 'Cancelled'},    # status là field, Cacelled là giá trị cụ thể của field
    order_by)
```
**Ex**
```bash
doc = frappe.get_last_doc('Article')
```

# get_all
```bash
frappe.get_all(
    "Article",
    filters={"status": "Available"},
    fields=["name", "author"]
)
```

# get_list
Lấy ra danh sách data.
**Ex**
```bash
frappe.get_list(
    "Article",
    filters={"status": "Available"},
    fields=["name", "publisher"],
    limit_page_length=5

-- SQL thuần --
frappe.db.sql("""
    SELECT name, status
    FROM `tabArticle`
    WHERE status = 'Available'
""", as_dict=True)
)
```
# delete_doc()
```bash
frappe.delete_doc(
    doctype='Article',
    name='My Third Book',
    force=True              # nếu muốn bỏ qua permission
```
**Ex**
```bash
frappe.delete_doc("Article", "Clean Code") # Clean Code là name trong doctype đó
```

4️⃣ Test validate / hook / msgprint
🔹 Test frappe.throw
doc = frappe.get_doc({
    "doctype": "Article",
    "article_name": "Bad ISBN",
    "isbn": "123",
    "status": "Available"
})
doc.insert()   # ❌ ValidationError

🔹 Test frappe.msgprint
frappe.clear_messages()

doc = frappe.get_doc({
    "doctype": "Article",
    "article_name": "No Publisher",
    "isbn": "1234567890",
    "status": "Available"
})
doc.insert()

frappe.get_messages()

5️⃣ Gọi API (@frappe.whitelist)
frappe.call(
    "book.book.doctype.article.article.my_api",
    arg1="hello"
)


Hoặc

from book.book.doctype.article.article import my_api
my_api("hello")

6️⃣ Quyền & user
🔹 Đổi user
frappe.set_user("Administrator")

frappe.set_user("test@example.com")

🔹 Bỏ qua permission (debug)
doc.insert(ignore_permissions=True)

7️⃣ Commit / Rollback DB

📌 

# Commit()
Trong console KHÔNG auto commit.
```bash
frappe.db.commit()
```

# Rollback()
```bash
frappe.db.rollback()
```
8️⃣ Debug nhanh
🔹 In ra log
frappe.log_error("Something wrong", "Article Debug")

# .as_dict()
```bash
print(doc.as_dict())
```
# .get_meta & .fields
Xem field của DocType.
```bash
frappe.get_meta("Article").fields
```

## .has_field()
Kiểm tra field tồn tại.
```bash
frappe.get_meta("Article").has_field("isbn")
```
🔟 Tiện ích hay dùng
frappe.now()
frappe.session.user
frappe.local.site