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
2. 02_structure_info.md (Cấu trúc & Kiểm tra nhanh)
    + Gom các thứ liên quan đến hình dáng DataFrame:
    + Nội dung: dataFrame.md, series.md, shape.md, columns.md, max_rows.md.
    + Ví dụ: Bạn mở file này khi cần xem cách tạo một cái khung dữ liệu mới hoặc kiểm tra xem nó có bao nhiêu dòng, cột.
3. 03_selection_filter.md (Lấy dữ liệu ra)
    + Gom các hàm dùng để "soi" dữ liệu:
    + Nội dung: loc.md, head.md, tail.md, where.md, notnull.md.
    + Lợi ích: Khi cần lọc dữ liệu theo điều kiện, bạn sẽ thấy loc và where nằm cạnh nhau để chọn phương án tối ưu.
4. 04_data_cleaning.md (Xử lý dữ liệu rác)
    + Đây là phần quan trọng nhất trong Pandas:
    + Nội dung: dropna.md, fillna.md, drop.md, duplicated-drop_duplicated.md, rename.md.
    + Lý do: Quy trình làm sạch thường là: Xóa dòng trống (dropna) -> Điền giá trị thiếu (fillna) -> Xóa trùng (drop_duplicated). Để chúng ở 3 folder khác nhau sẽ làm ngắt quãng tư duy xử lý.
5. 05_transformation.md (Biến đổi nâng cao)
    + Gom các thao tác làm thay đổi bản chất dữ liệu hoặc gộp nhóm:
    + Nội dung: merge.md, sort_values.md, value_counts.md, nunique.md, astype.md.
    + Cách xử lý "Ví dụ thực tế" trong Pandas:
```
# Cài đặt
```bash
- Thường dùng để xử lý dữ liệu. Pandas kế thừa numpy tức là nó có thể sử dụng hầu hết các hàm trong numpy
- pip install pandas / conda install pandas.
```
# Bài tập
## Demo bài 1
**Topic**
```bash
Quản lý danh sách công nhân gồm:
- id – mã công nhân
- name – họ tên
- salary – lương ngày
- days_work – số ngày làm việc
- allowance – phụ cấp
Yêu cầu:
- Tạo DataFrame
- Tính tổng lương
- Lọc công nhân có tổng lương > 15 triệu
- Đếm số công nhân thỏa điều kiện
- Sắp xếp theo tổng lương giảm dần
- Sửa phụ cấp theo điều kiện
- Xóa công nhân có lương = 0
- Ghi ra file CSV
```
```python
import pandas as pd

def input_workers():
    n = int(input("Số lượng công nhân: "))
    
    data = []
    for i in range(n):
        print(f"\nNhập công nhân thứ {i+1}")

        worker = {
            'worker_id': input('Mã công nhân: '),
            'name': input('Họ tên: '),
            'days_work': float(input('Số ngày làm việc: ')),
            'salary': float(input('Lương ngày: ')),
            'sum_salary': None
        }

        data.append(worker)

    df = pd.DataFrame(data)

    return df

def calculate_salary(df):
    df['sum_salary'] = df['salary'] * df['days_work'] + df['allowance']
    print("\n=== Đã tính tổng lương ===")
    print(df)

def filter_high_salary(df):
    df_high = df[df['sum_salary'] > 15_000_000]
    print("\n=== Công nhân có thu nhập > 15 triệu ===")
    print(df_high)
    print("Số lượng:", df_high.shape[0])

def sort_by_salary(df):
    df_sorted = df.sort_values(by='sum_salary', ascending=False)
    print("\n=== Danh sách sắp xếp theo tổng lương giảm dần ===")
    print(df_sorted)
    return df_sorted

def update_allowance(df):
    df.loc[df['days_work'] > 26, 'allowance'] += 200_000
    df['sum_salary'] = df['salary'] * df['days_work'] + df['allowance']
    print("\n=== Đã cập nhật phụ cấp ===")
    print(df)

def delete_zero_salary(df):
    df = df[df['salary'] != 0]
    print("\n=== Sau khi xóa công nhân có lương = 0 ===")
    print(df)
    return df

def save_csv(df):
    df.to_csv("cong_nhan.csv", index=False, encoding="utf-8-sig")
    print("\nĐã ghi file cong_nhan.csv")


def main():
    df = None

    print("=== MENU ===")
    print("0. Thoát")
    print("1. Nhập danh sách công nhân")
    print("2. Tính tổng lương")
    print("3. Lọc & đếm thu nhập > 15 triệu")
    print("4. Sắp xếp theo tổng lương")
    print("5. Sửa phụ cấp")
    print("6. Xóa công nhân lương = 0")
    print("7. Ghi ra file CSV")

    while True:
        option = int(input("\nChọn chức năng: "))

        if option == 0:
            break
        elif option == 1:
            df = input_workers()
            print(df)
        elif option == 2:
            calculate_salary(df)
        elif option == 3:
            filter_high_salary(df)
        elif option == 4:
            df = sort_by_salary(df)
        elif option == 5:
            update_allowance(df)
        elif option == 6:
            df = delete_zero_salary(df)
        elif option == 7:
            save_csv(df)


main()
```

## Bài tập 2
```python
import pandas as pd

# ===== KHỞI TẠO DATAFRAME =====
def init_df():
    return pd.DataFrame(
        columns=["worker_id", "name", "salary", "days_work", "allowance", "sum_salary"]
    )


# ===== NHẬP DANH SÁCH =====
def input_workers():
    n = int(input("Số lượng công nhân: "))
    data = []

    for i in range(n):
        print(f"--- Công nhân {i+1} ---")
        wid = input("Mã: ")
        name = input("Họ tên: ")
        salary = float(input("Lương/ngày: "))
        days = int(input("Số ngày làm: "))
        allowance = float(input("Phụ cấp: "))

        data.append({
            "worker_id": wid,
            "name": name,
            "salary": salary,
            "days_work": days,
            "allowance": allowance,
            "sum_salary": salary * days + allowance
        })

    return pd.DataFrame(data)

# ===== IN BẢNG =====
def print_table(df):
    if df.empty:
        print("Danh sách rỗng")
    else:
        print(df.to_string(index=False))


# ===== THÊM CÔNG NHÂN =====
def add_worker(df):
    wid = input("Mã: ")
    name = input("Họ tên: ")
    salary = float(input("Lương/ngày: "))
    days = int(input("Số ngày làm: "))
    allowance = float(input("Phụ cấp: "))

    new_row = {
        "worker_id": wid,
        "name": name,
        "salary": salary,
        "days_work": days,
        "allowance": allowance,
        "sum_salary": salary * days + allowance
    }

    return pd.concat([df, pd.DataFrame([new_row])], ignore_index=True)


# ===== TÍNH LẠI LƯƠNG =====
def calc_salary(df):
    df["sum_salary"] = df["salary"] * df["days_work"] + df["allowance"]


# ===== SỬA THEO MÃ =====
def update_worker(df):
    wid = input("Nhập mã cần sửa: ")

    if wid not in df["worker_id"].values:
        print("Không tìm thấy!")
        return

    df.loc[df["worker_id"] == wid, "salary"] = float(input("Lương mới: "))
    df.loc[df["worker_id"] == wid, "days_work"] = int(input("Ngày làm mới: "))
    df.loc[df["worker_id"] == wid, "allowance"] = float(input("Phụ cấp mới: "))

    calc_salary(df)


# ===== XÓA THEO MÃ =====
def delete_worker(df):
    wid = input("Nhập mã cần xóa: ")
    return df[df["worker_id"] != wid]


# ===== LỌC + ĐẾM =====
def filter_high_salary(df):
    df_high = df[df["sum_salary"] > 15_000_000]
    print("\n=== Thu nhập > 15 triệu ===")
    print_table(df_high)
    print("Số lượng:", len(df_high))


# ===== SẮP XẾP =====
def sort_by_salary(df):
    return df.sort_values(by="sum_salary", ascending=False)


# ===== GHI FILE CSV =====
def save_to_csv(df):
    df.to_csv("workers.csv", index=False)
    print("Đã ghi file workers.csv")


# ===== MENU =====
def main():
    df = init_df()

    while True:
        print("""
0. Thoát
1. Nhập danh sách
2. In danh sách
3. Tính lương
4. Thêm công nhân
5. Sửa công nhân
6. Xóa công nhân
7. Lọc thu nhập > 15 triệu
8. Sắp xếp theo lương giảm dần
9. Ghi ra file CSV
""")
        choice = int(input("Chọn: "))

        if choice == 0:
            break
        elif choice == 1:
            df = input_workers()
        elif choice == 2:
            print_table(df)
        elif choice == 3:
            calc_salary(df)
            print("Đã tính lương")
        elif choice == 4:
            df = add_worker(df)
        elif choice == 5:
            update_worker(df)
        elif choice == 6:
            df = delete_worker(df)
        elif choice == 7:
            filter_high_salary(df)
        elif choice == 8:
            df = sort_by_salary(df)
            print("Đã sắp xếp")
        elif choice == 9:
            save_to_csv(df)


main()
```