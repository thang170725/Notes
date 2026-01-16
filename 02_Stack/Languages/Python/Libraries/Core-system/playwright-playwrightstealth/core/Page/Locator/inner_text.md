# locator.inner_text()
```bash
Tác dụng: Lấy nội dung chữ bên trong một phần tử.
```
**Syn**
```bash
chu = await element.inner_text()
```
**Ex**
```python
doan_van = page.locator("p") # Giả sử có thẻ <p>Chào bạn</p>
noidung = await doan_van.inner_text()
print(noidung) # Kết quả: Chào bạn
```