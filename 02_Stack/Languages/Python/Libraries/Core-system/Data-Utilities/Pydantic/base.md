- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
---
```bash
- Trong Python thông thường, bạn có thể truyền bất cứ thứ gì vào một đối tượng. Với Pydantic, bạn tạo ra một "khung bảo vệ". Dữ liệu đi vào phải đi qua cái khung này:
  + Nếu đúng kiểu: Nó được chấp nhận.
  + Nếu sai kiểu nhưng có thể sửa: Nó sẽ tự động được ép kiểu (ví dụ chuỗi "10" thành số 10).
  + Nếu sai hoàn toàn: Nó sẽ chặn lại và báo lỗi chi tiết.

- Cần pip install pydantic

- Pydantic là 'vị vua' trong thế giới API, nhưng ít khi được sử dụng trong lõi tính toán trong AI/Data Science
```
# Cấu trúc thư mục
```bash
Pydantic/
├── 01_models_fields.md      # Định nghĩa Model: BaseModel, Field, Alias, Type Hinting
├── 02_validators.md         # Kiểm tra dữ liệu: @field_validator, @model_validator
├── 03_serialization.md      # Xuất dữ liệu: model_dump, model_dump_json, ConfigDict
├── 04_data_types.md         # Các kiểu dữ liệu đặc biệt: EmailStr, HttpUrl, SecretStr
└── 05_settings_management.md # Quản lý cấu hình: BaseSettings, .env loading
```
**Chi tiết**
```bash
1. 01_models_fields.md (Khai báo)
  + Đây là nơi chứa các hàm định nghĩa cấu trúc bảng.
  + Hàm chính: BaseModel, Field().
  + Nội dung: Cách đặt giá trị mặc định, giới hạn độ dài chuỗi (min_length, max_length), giới hạn giá trị số (gt, lt), và đặt tên giả (alias).
Lý do: Bạn mở file này khi muốn tạo một Schema mới.
2. 02_validators.md (Kiểm tra logic)
  + Nơi chứa các hàm kiểm tra điều kiện phức tạp mà Field không làm được.
  + Hàm chính: @field_validator (cho từng trường), @model_validator (cho cả bảng).
  + Ví dụ: Kiểm tra xem mật khẩu và xác nhận mật khẩu có khớp nhau không.
3. 03_serialization.md (Chuyển đổi đầu ra)
  + Hàm chính: model_dump(), model_dump_json(), model_validate(), ConfigDict.
  + Nội dung: Cách cấu hình from_attributes=True (để Pydantic đọc được dữ liệu từ SQLAlchemy Object).
  + Lý do: Bạn mở file này khi cần biến đối tượng Model thành Dictionary hoặc JSON để trả về API.
4. 04_data_types.md (Kiểu dữ liệu xịn)
  + Pydantic có những kiểu dữ liệu cực hay mà Python thuần không có.
  + Các kiểu: EmailStr (tự check định dạng mail), HttpUrl (check link), IPvAnyAddress, SecretStr (ẩn giá trị khi in log).
  + Lưu ý: Ghi chú cách cài pydantic[email] để dùng được EmailStr.
5. 05_settings_management.md (Cấu hình hệ thống)
  + Sử dụng gói pydantic-settings.
  + Hàm chính: BaseSettings.
  + Nội dung: Cách đọc các biến môi trường từ file .env vào Python.
  + Lý do: Đây là cách chuyên nghiệp nhất để quản lý API Key, Database URL trong dự án.
```