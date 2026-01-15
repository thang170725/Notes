```bash
- Trong phiên bản Frappe UI (v0.1.248), createResource là công cụ cơ bản và linh hoạt nhất để quản lý việc truy xuất dữ liệu từ server hoặc các API bên ngoài. Khác với các công cụ chuyên biệt như createListResource (dùng cho danh sách) hay createDocumentResource (dùng cho một bản ghi), createResource được dùng cho các yêu cầu API tổng quát.
- Lưu ý quan trọng cho phiên bản của bạn
    + Whitelisting: Các hàm Python được gọi qua url phải được đánh dấu @frappe.whitelist() ở phía backend để có thể truy cập từ frontend.
    + ignore_csrf: Trong môi trường phát triển local (Vite), bạn cần thêm "ignore_csrf": 1 vào file site_config.json để tránh lỗi bảo mật khi gọi API.
    + Phân biệt: Nếu bạn chỉ làm việc với danh sách DocType chuẩn, hãy cân nhắc dùng createListResource vì nó hỗ trợ sẵn các phương thức phân trang như next() và previous() tiện lợi hơn.
- createResource giống như một "đường dây nóng" đa năng. Trong khi các công cụ khác chỉ chuyên dùng để gọi "cảnh sát" (danh sách) hoặc "cứu hỏa" (bản ghi đơn lẻ), thì createResource cho phép bạn gọi đến bất kỳ căn phòng nào trong tòa nhà (backend) miễn là căn phòng đó cho phép bạn kết nối
```
**Syn**
```js
import { createResource } from 'frappe-ui'

const myResource = createResource({
  url: 'dotted.path.to.python.method', // Đường dẫn đến hàm Python (ví dụ: 'frappe.client.get_list') [2, 5]
  method: 'POST', // Phương thức HTTP (mặc định thường là POST cho các hàm Frappe) [2, 6]
  params: {
    // Các tham số truyền vào hàm [2, 5]
  },
  auto: true, // Nếu true, resource sẽ tự động thực hiện yêu cầu khi component được khởi tạo [2, 4]
  cache: 'my_cache_key', // (Tùy chọn) Lưu bộ nhớ đệm trong IndexedDB [7, 8]
  onSuccess(data) {
    // Xử lý khi thành công [4, 9]
  },
  onError(error) {
    // Xử lý khi gặp lỗi [4, 9]
  }
})
```

# .data
Chứa kết quả trả về từ API.

# .loading
Giá trị boolean, true nếu yêu cầu đang được thực hiện.

# .error
Chứa thông tin lỗi nếu yêu cầu thất bại.

# .fetched
Giá trị boolean, true nếu dữ liệu đã được lấy thành công ít nhất một lần.
Các phương thức điều khiển:
• fetch(): Kích hoạt yêu cầu lấy dữ liệu thủ công.
• reload(): Làm mới dữ liệu (tương tự fetch).
• submit(values): Thường dùng cho các yêu cầu thay đổi dữ liệu (POST/PUT), cho phép truyền tham số mới.

## Demo đơn giản nhất
```bash
Giả sử bạn muốn lấy thông tin một bản ghi ToDo cụ thể bằng cách gọi hàm frappe.client.get_list thông qua createResource
```
```js
import { createResource } from 'frappe-ui'

const todo = createResource({
  url: 'frappe.client.get_list',
  params: {
    doctype: 'ToDo',
    fields: ['description', 'status', 'name'],
    filters: { name: '0489l150rq' }
  },
  auto: true

<template>
  <div v-if="todo.loading">Đang tải...</div>
  <div v-else-if="todo.data">
    <!-- Giả định kết quả trả về là một mảng -->
    <h3>{{ todo.data?.description }}</h3>
    <p>Trạng thái: {{ todo.data?.status }}</p>
  </div>
  <div v-if="todo.error">Lỗi: {{ todo.error }}</div>
</template>

- Khi todo.data được nạp thành công, cấu trúc dữ liệu sẽ trông như sau:
[
  {
    "description": "Nội dung công việc",
    "status": "Open",
    "name": "0489l150rq"
  }
]
```
