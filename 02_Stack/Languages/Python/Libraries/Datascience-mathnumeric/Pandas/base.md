- [Cấu trúc đề xuất](#cấu-trúc-đề-xuất)
- [Cài đặt](#cài-đặt)
- [Bài tập](#bài-tập)
  - [Demo bài 1](#demo-bài-1)
  - [Bài tập 2](#bài-tập-2)
---
# Cấu trúc đề xuất
```bash
Pandas/
├── 01_io_conversion.md       # Nhập/Xuất & Chuyển đổi (Read, Write, Coercion)
├── 02_structure_info.md      # Khởi tạo & Thông tin (Create, Size, base, dtypes)
├── 03_selection_filter.md    # Trích xuất & Lọc (Loc, Head/Tail, Check, Where)
├── 04_data_cleaning.md       # Làm sạch & Cập nhật (Drop, Fillna, Duplicated, Rename)
└── 05_transformation.md      # Biến đổi & Thống kê (Merge, Sort, Value_counts, Astype)
```
**Chi tiết cách gộp nội dung:**
```bash
1. 01_io_conversion.md (Đọc, Ghi & Ép kiểu)
    + Gom các thao tác đưa dữ liệu vào và ra:
    + Nội dung: read_csv, read_sql, to_csv, to_sql, values-to_numpy.
    + Lý do: Khi bạn làm việc với File hoặc SQL, bạn thường quan tâm đến việc đọc vào và ghi ra ở cùng một chỗ để kiểm tra tính nhất quán.
2. 02_structure_info.md (Khai báo & xem tổng quan & kiểm tra để biết)
    + Gom các thứ liên quan đến hình dáng DataFrame:
3. 03_selection_filter.md (Lấy dữ liệu cần thiết & kiểm tra để lọc)
4. 04_data_cleaning.md (dọn rác & sửa tên & kiểm tra để làm sạch)
5. 05_transformation.md (Biến đổi nâng cao & kiểm tra để phân tích)
    + Biến đổi, Thống kê & Liên kết (Gộp bảng, Ép kiểu, Thống kê số liệu)
```
# Cài đặt
```bash
- Thường dùng để xử lý dữ liệu. Pandas kế thừa numpy tức là nó có thể sử dụng hầu hết các hàm trong numpy
- pip install pandas / conda install pandas.
```
