```text
Trong Frappe Framework, frappe.msgprint và frappe.throw đều dùng để hiển thị thông báo cho người dùng, nhưng mục đích và hành vi khác nhau. 
```

# frappe.msgprint 
- Hiển thị thông báo (KHÔNG dừng chương trình)
- Dùng khi nào?
    + Thông báo thành công
    + Nhắc nhở
    + Debug nhanh
    + Không làm gián đoạn xử lý

**Syn**
```bash
frappe.msgprint("Nội dung thông báo")
```
```python
import frappe
from frappe.model.document import Document

class Article(Document):

    def validate(self):
        self.validate_isbn()
        self.warn_if_no_publisher()

    def validate_isbn(self):
        if self.isbn and len(self.isbn) < 10:
            frappe.throw("ISBN phải có ít nhất 10 ký tự")

    def warn_if_no_publisher(self):
        if not self.publisher:
            frappe.msgprint(
                msg="Bạn chưa nhập Publisher",
                title="Cảnh báo",
                indicator="orange"
            )
```

# frappe.throw 
```text
- Ném lỗi (DỪNG chương trình ngay)
- Dùng khi nào?
    + Validate dữ liệu
    + Ngăn không cho lưu
    + Trả lỗi về frontend (HTTP 417 / 400)
```
**Syn**
```bash
frappe.throw("Nội dung lỗi")
```
```python
import frappe
from frappe.model.document import Document

class Article(Document):

    def validate(self):
        # validate trước khi lưu (insert & update)
        self.validate_isbn()
        self.validate_status()

    def validate_isbn(self):
        if self.isbn and len(self.isbn) < 10:
            frappe.throw("ISBN phải có ít nhất 10 ký tự")

    def validate_status(self):
        if self.status not in ["Issued", "Available"]:
            frappe.throw("Status không hợp lệ")
```