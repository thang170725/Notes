```bash
- *row dùng để trải các phần tử của list ra thành nhiều đối số cho print(), giúp in đẹp đúng format ma trận.
```
**Ex: Không dùng *row**
```python
row = [1, 2, 3]

print(row) # [1, 2, 3]. Không đúng định dạng đề bài (có dấu [ ] và dấu ,)
print(*row) # 1 2 3. Đúng định dạng mỗi phần tử cách nhau bằng dấu cách
```