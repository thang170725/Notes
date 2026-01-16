```bash
- Trong Python thông thường, bạn có thể truyền bất cứ thứ gì vào một đối tượng. Với Pydantic, bạn tạo ra một "khung bảo vệ". Dữ liệu đi vào phải đi qua cái khung này:
  + Nếu đúng kiểu: Nó được chấp nhận.
  + Nếu sai kiểu nhưng có thể sửa: Nó sẽ tự động được ép kiểu (ví dụ chuỗi "10" thành số 10).
  + Nếu sai hoàn toàn: Nó sẽ chặn lại và báo lỗi chi tiết.

- Cần pip install pydantic

- Pydantic là 'vị vua' trong thế giới API, nhưng ít khi được sử dụng trong lõi tính toán trong AI/Data Science
```