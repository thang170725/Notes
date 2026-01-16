# locator.nth(index)
```bash
- Tác dụng: Chọn phần tử thứ n trong danh sách các phần tử tìm được (bắt đầu từ số 0).
```
**Syn** 
```bash
item = element.nth(0) (lấy phần tử đầu tiên).
```
**Ex**
```python
danh_sach = page.locator("li")
thu_nhat = danh_sach.nth(0) # Lấy dòng đầu tiên trong danh sách
```