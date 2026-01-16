# locator.count()
```bash
- Tác dụng: Đếm xem có bao nhiêu phần tử khớp với locator đã tìm.
```
**Syn** 
```bash
so_luong = await element.count()
```
**Ex**
```python
cac_nut = page.locator("button")
print(await cac_nut.count()) # In ra số lượng nút bấm có trên trang
```