- [.loading](#loading)
- [.error: Chứa thông tin lỗi nếu truy vấn thất bại.](#error-chứa-thông-tin-lỗi-nếu-truy-vấn-thất-bại)
  - [crud bằng creatListView](#crud-bằng-creatlistview)
    - [Read (đọc dữ liệu)](#read-đọc-dữ-liệu)
  - [Create (thêm mới bản ghi)](#create-thêm-mới-bản-ghi)
  - [Update (cập nhật bản ghi)](#update-cập-nhật-bản-ghi)
  - [Delete (Xóa bản ghi)](#delete-xóa-bản-ghi)

---

```bash
Trong bộ công cụ Frappe UI (phiên bản v0.1.248 mà bạn đang sử dụng), khái niệm "ListView" thường được hiểu theo hai khía cạnh: - thành phần giao diện (UI Component) để hiển thị danh sách và bộ công cụ xử lý dữ liệu (Resource) để lấy danh sách từ backend.
Dưới đây là chi tiết về cách sử dụng dựa trên các nguồn tài liệu:
- ListView dùng để:
    +  Hiển thị bộ sưu tập các bản ghi (documents) từ một DocType cụ thể trong giao diện người dùng.
    +  Hỗ trợ tương tác: Cho phép người dùng tìm kiếm, lọc, sắp xếp và phân trang dữ liệu một cách hiệu quả.
    +  Quản lý trạng thái dữ liệu: Tự động xử lý các trạng thái đang tải (loading), lỗi (error) và cập nhật dữ liệu khi có thay đổi từ server.
- Lưu ý quan trọng cho phiên bản v0.1.248
    + CSRF Protection: Khi phát triển local với Vite (thường chạy cổng 8080), bạn cần thiết lập "ignore_csrf": 1 trong file site_config.json của Frappe để tránh lỗi bảo mật khi fetch dữ liệu.
    + Tính kế thừa: Phiên bản này sử dụng hệ thống Espresso Design, do đó các thành phần như Button hay Table sẽ có các thuộc tính (props) đồng nhất như variant (v dụ: 'subtle', 'solid') và theme (ví dụ: 'gray', 'primary').
Ví dụ tương tự: Hãy tưởng tượng createListResource giống như một "nhân viên phục vụ" đứng giữa bạn và nhà bếp (backend). Bạn đưa cho họ một danh sách yêu cầu (fields, filters), và họ sẽ tự động lo việc bưng món ăn ra (data), thông báo khi bếp đang nấu (loading), hoặc báo nếu nhà bếp hết món (error). ListView chính là cái bàn nơi các món ăn đó được trình bày ngăn nắp cho bạn thưởng thức.
```
**Syn**
```bash
Trong Frappe UI, để xây dựng một ListView, bạn cần kết hợp giữa việc lấy dữ liệu (createListResource) và hiển thị dữ liệu trên giao diện Vue 3.
```
```js
import { createListResource } from 'frappe-ui'

// Khởi tạo resource để lấy danh sách ToDo
const todos = createListResource({
  doctype: 'ToDo', // Tên DocType cần lấy
  fields: ['name', 'description', 'status', 'date'], // Các trường dữ liệu muốn hiển thị [6]
  filters: {
    status: 'Open', // Bộ lọc (ví dụ: chỉ lấy các việc đang mở) [7]
  },
  orderBy: 'creation desc', // Sắp xếp theo ngày tạo giảm dần [3]
  pageLength: 10, // Số lượng bản ghi trên mỗi trang [3]
  auto: true, // Tự động fetch dữ liệu khi component được mount
})
```
```js
<template>
  <div>
    <!-- Hiển thị trạng thái đang tải -->
    <p v-if="todos.loading">Đang tải dữ liệu...</p>

    <!-- Hiển thị danh sách nếu có dữ liệu -->
    <ul v-if="todos.data">
      <li v-for="item in todos.data" :key="item.name">
        {{ item.description }} - <strong>{{ item.status }}</strong>
      </li>
    </ul>

    <!-- Nút phân trang -->
    <div class="flex gap-2">
      <button @click="todos.previous()" :disabled="!todos.hasPreviousPage">Trang trước</button>
      <button @click="todos.next()" :disabled="!todos.hasNextPage">Trang sau</button>
    </div>
  </div>
</template>

- Khi gọi todos.fetch() hoặc khi auto: true, resource sẽ trả về một đối tượng có cấu trúc dữ liệu như sau để bạn sử dụng:
Dữ liệu trong todos.data:
[
  {
    "name": "0489l150rq",
    "description": "Họp nhóm dự án",
    "status": "Open",
    "date": "2025-01-14"
  },
  {
    "name": "0489l150r1",
    "description": "Viết báo cáo tuần",
    "status": "Closed",
    "date": "2025-01-13"
  }
]
```

# .loading
true khi đang gọi API, false khi đã xong.

# .error: Chứa thông tin lỗi nếu truy vấn thất bại.
• todos.hasNextPage: true nếu còn dữ liệu ở trang tiếp theo.

## crud bằng creatListView
```bash
Đây là cách tốt nhất khi bạn muốn quản lý một danh sách bản ghi và thêm mới dữ liệu vào danh sách đó.
  + Đọc danh sách (Read):
  + Thêm mới (Create):
  + Ghi chú: Phương thức insert thuộc List Resource sẽ tự động gửi dữ liệu lên server
```
### Read (đọc dữ liệu)
```bash
Để đọc danh sách hoặc một bản ghi cụ thể, bạn sử dụng createListResource hoặc createDocumentResource.
```
```bash
import { createListResource, createDocumentResource } from 'frappe-ui'

// 1.1 Đọc danh sách ToDo
const todos = createListResource({
  doctype: 'ToDo',
  fields: ['name', 'description', 'status'],
  auto: true, // Tự động lấy dữ liệu khi component nạp [1], [2]
})

// 1.2 Đọc một bản ghi cụ thể theo "name"
const todoDetail = createDocumentResource({
  doctype: 'ToDo',
  name: '0489l150rq',
  auto: true,
})
```

## Create (thêm mới bản ghi)
```bash
function createNewTodo() {
  todos.insert.submit({
    description: 'Nhiệm vụ mới từ Demo',
    status: 'Open',
  }).then((doc) => {
    console.log('Đã tạo bản ghi:', doc)
    todos.reload() // Làm mới danh sách sau khi thêm [3]
  })
}
```

## Update (cập nhật bản ghi)
Để sửa đổi, bạn sử dụng Document Resource. Quy trình gồm hai bước: đặt giá trị mới (setValue) và lưu lại (save),.
function updateTodoStatus() {
  // Gán giá trị mới cho trường 'status'
  todoDetail.setValue.submit({
    status: 'Closed'
  }).then(() => {
    // Sau khi set value, gọi save để gửi lên server [3], [4]
    todoDetail.save.submit()
  })
}

## Delete (Xóa bản ghi)
Xóa bản ghi được thực hiện trực tiếp thông qua phương thức delete của Document Resource,.
function deleteThisTodo() {
  if (confirm('Bạn có chắc muốn xóa?')) {
    todoDetail.delete.submit().then(() => {
      console.log('Đã xóa thành công')
      // Thường sẽ chuyển hướng trang hoặc cập nhật lại danh sách cha
    })
  }
}