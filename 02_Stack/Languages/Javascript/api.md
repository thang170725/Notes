- [async \& fetch](#async--fetch)
  - [GET data JSON bằng async + fetch](#get-data-json-bằng-async--fetch)
  - [POST data JSON bằng async + fetch](#post-data-json-bằng-async--fetch)
- [FormData() \& .blob() \& URL.createObjectURL()](#formdata--blob--urlcreateobjecturl)
    - [Demo POST ảnh về server xử lý rồi lại chuyển lại về giao diện](#demo-post-ảnh-về-server-xử-lý-rồi-lại-chuyển-lại-về-giao-diện)
---
## API trong Javascript
Cách viết Promise
Đây là cách viết xử lý API truyền thống bằng chuỗi promise.

Ví dụ:
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
# async & fetch
```bash
- fetch : Là một API dùng để gửi các yêu cầu HTTP (GET, POST, PUT, DELETE, …) đến server và xử lý kết quả trả về. 
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