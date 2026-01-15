- [FormData() \& .blob() \& URL.createObjectURL()](#formdata--blob--urlcreateobjecturl)
    - [Demo POST ảnh về server xử lý rồi lại chuyển lại về giao diện](#demo-post-ảnh-về-server-xử-lý-rồi-lại-chuyển-lại-về-giao-diện)


---

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