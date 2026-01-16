# locator.get_attribute(name)
```bash
- Tác dụng: Lấy giá trị của một thuộc tính trong thẻ (thường dùng nhất là lấy link href hoặc link ảnh src).
```
**Syn** 
```bash
gia_tri = await element.get_attribute("tên_thuộc_tính")
```
**Ex**
```python
the_link = page.locator("a") # Lấy đường link của một thẻ <a>
url = await the_link.get_attribute("href")
print(url)
```