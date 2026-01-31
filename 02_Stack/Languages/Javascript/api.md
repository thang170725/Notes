- [Promise](#promise)
- [async \& fetch](#async--fetch)
  - [GET data JSON bằng async + fetch](#get-data-json-bằng-async--fetch)
  - [POST data JSON bằng async + fetch](#post-data-json-bằng-async--fetch)
- [FormData() \& .blob() \& URL.createObjectURL()](#formdata--blob--urlcreateobjecturl)
    - [Demo POST ảnh về server xử lý rồi lại chuyển lại về giao diện](#demo-post-ảnh-về-server-xử-lý-rồi-lại-chuyển-lại-về-giao-diện)
- [localStorage](#localstorage)
- [.setItem() \& .getItem() \& .removeItem() \& .clear()](#setitem--getitem--removeitem--clear)
---
# Promise
```bash
Đây là cách viết xử lý API truyền thống bằng chuỗi promise.
```
**Ex**
```js
// 1. Tạo dữ liệu muốn gửi đi
const data = {
  message: "Xin chào AI!"
};

// 2. Gọi API bằng fetch
fetch('http://localhost:5000/api', {
  method: 'POST',                    // 3. Gửi dữ liệu bằng phương thức POST
  headers: {
    'Content-Type': 'application/json'  // 4. Báo cho server biết dữ liệu gửi đi là JSON
  },
  body: JSON.stringify(data)         // 5. Chuyển object `data` thành chuỗi JSON để gửi đi
})

// 6. Khi nhận được phản hồi, chuyển phản hồi thành JSON
.then(response => response.json())

// 7. In kết quả ra console
.then(result => {
  console.log('Phản hồi từ server:', result);
})

// 8. Nếu có lỗi trong quá trình gọi API
.catch(error => {
  console.error('Lỗi khi gọi API:', error);
});
```
# async & fetch
```bash
- fetch : Là một API dùng để gửi các yêu cầu HTTP (GET, POST, PUT, DELETE, …) đến server và xử lý kết quả trả về. 
```
**Syn**
```bash
fetch("https://api.example.com/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ name: "Thắng" }),
})

- method
  + "GET" | "POST" | "PUT" | "PATCH" | "DELETE"
  + Mặc định: "GET"
  + Quyết định bạn đang làm gì với server
- headers
  + Là metadata của request → cho server biết: Dữ liệu kiểu gì
  + Ai gửi
  + Quyền hạn gì
  + Header là key – value (string)
- body
  + Dữ liệu gửi lên server
  + Chỉ dùng với POST / PUT / PATCH. Không dùng với GET (chuẩn REST)

4. credentials
credentials: "include"

Giá trị	Ý nghĩa
"omit"	Không gửi cookie
"same-origin"	Chỉ gửi cookie cùng domain
"include"	Luôn gửi cookie

📌 Dùng khi:

login bằng cookie

session-based auth

5. mode
mode: "cors"

Giá trị	Khi nào
"cors"	Gọi API khác domain
"same-origin"	Cùng domain
"no-cors"	Gần như không dùng
6. cache
cache: "no-cache"


Điều khiển cache của browser

7. signal (huỷ request)
const controller = new AbortController()

fetch(url, {
  signal: controller.signal
})

controller.abort()


👉 Dùng khi:

user rời trang

search realtime

5️⃣ Xử lý response từ fetch
const response = await fetch(url)

response có gì?
Thuộc tính	Ý nghĩa
response.ok	status 200–299
response.status	HTTP status
response.headers	headers trả về
Đọc body response
JSON
const data = await response.json()

Text
const text = await response.text()

6️⃣ Ví dụ THỰC TẾ HOÀN CHỈNH
async function login(username, password) {
  const response = await fetch("/login", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({ username, password }),
  })

  if (!response.ok) {
    throw new Error("Login failed")
  }

  return response.json()
}

7️⃣ Những lỗi người mới hay gặp ⚠️
❌ Quên JSON.stringify
body: { username, password } // SAI

❌ Gửi body với GET
fetch("/users", { body: "{}" }) // SAI

❌ Quên check response.ok
await response.json() // có thể crash

8️⃣ Nếu bạn chỉ nhớ 3 điều

1️⃣ fetch(url, options)
2️⃣ method + headers + body là 3 cái quan trọng nhất
3️⃣ fetch KHÔNG tự báo lỗi HTTP

Nếu bạn muốn, mình có thể:

🧠 Vẽ sơ đồ request–response

🔥 So sánh fetch vs axios

🧪 Viết wrapper fetch chuẩn production

⚠️ Chỉ ra bug thường gặp khi dùng fetch

Bạn muốn tiếp hướng nào?
```
## GET data JSON bằng async + fetch
```js
async function getUsers() {
  try {
    const response = await fetch(
      'https://jsonplaceholder.typicode.com/users'
    )

    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`)
    }

    const data = await response.json()
    console.log(data)
  } catch (err) {
    console.error(err)
  }
}

getUsers()
```
## POST data JSON bằng async + fetch
```js
aasync function createUser() {
  try {
    const response = await fetch(
      'https://jsonplaceholder.typicode.com/users',
      {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          name: 'Le Duc Thang',
          email: 'thang@gmail.com'
        })
      }
    )

    if (!response.ok) {
      throw new Error(`POST failed: ${response.status}`)
    }

    const data = await response.json()
    console.log(data)
  } catch (err) {
    console.error(err)
  }
}

createUser()
```
# FormData() & .blob() & URL.createObjectURL()
**FormData**
```bash
- Là một đối tượng giúp bạn tạo ra các cặp key-value giống như dữ liệu trong form HTML, để gửi đi bằng fetch hoặc XMLHttpRequest.
- Nó dùng được cho text, file (ảnh, pdf, …)
- Cần gửi với Content-Type: multipart/form-data
```
**.blob()**
```bash
Là một đối tượng dùng để lưu trữ dữ liệu nhị phân
```


### Demo POST ảnh về server xử lý rồi lại chuyển lại về giao diện
**html**
```html
<div class='send-image'>
    <input type="file" class='image-input' accept="image/">
    <button onclick='upload()'>Upload</button>
</div>
<div class='result'></div>
```
**js**
```js
async function upload() {
    const fileInput = document.getElementsByClassName('image-input')[0];
    const file = fileInput.files[0];
    if (!file) return alert("don't choose image");
    const formData = new FormData();
    formData.append('image', file);
    formData.append('author', 'thangle');
    const res = await fetch('http://127.0.0.1:8000/user/image-grayscale', {
        method: 'POST',
        body: formData
    })
    const blob = await res.blob()
    const imageUrl = URL.createObjectURL(blob)
    document.querySelector(".result").innerHTML = `
        <h3>Result</h3>
        <img src="${imageUrl}" />
    `
}
```
# localStorage 
```bash
- Dùng để lưu dữ liệu ngay trên trình duyệt. -> Dung lượng khoảng 5–10MB
- Dữ liệu không mất khi refresh trang hoặc tắt trình duyệt
- Chỉ lưu được chuỗi (string)
```
# .setItem() & .getItem() & .removeItem() & .clear()
```bash
- setItem     : Để lưu dữ liệu.
- getItem     : Để lấy dữ liệu.
- removeItem  : Xóa 1 dữ liệu ở localStorage.
- clear       : Xóa tất cả dữ liệu.
```
**Ex: Lưu tên người dùng**
```html
<input type="text" id="nameInput" placeholder="Nhập tên">
<button onclick="saveName()">Lưu tên</button>
<button onclick="getName()">Lấy tên</button>
<button onclick="removeName()">Xoá tên</button>
<button onclick="clearAll()">Clear tất cả</button>

<p id="result"></p>
```
```js
function saveName() {
  const name = document.getElementById("nameInput").value;
  localStorage.setItem("username", name);
  alert("Đã lưu tên!");
}

function getName() {
  const name = localStorage.getItem("username");
  document.getElementById("result").innerText =
    name ? "Tên đã lưu: " + name : "Chưa có tên!";
}

function removeName() {
  localStorage.removeItem("username");
  alert("Đã xoá tên!");
}

function clearAll() {
  localStorage.clear();
  alert("Đã xoá toàn bộ localStorage!");
}
```
**Ex2: lưu object / array**
```js
const user = {
  name: "Thắng",
  age: 22
};

localStorage.setItem("user", JSON.stringify(user));
```
**Ex3: lấy object**
```js
const user = JSON.parse(localStorage.getItem("user"));
console.log(user.name); // Thắng
```