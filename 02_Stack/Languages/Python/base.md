- [Kiểm tra](#kiểm-tra)
- [Tạo môi trường ảo \& activate](#tạo-môi-trường-ảo--activate)
- [deactivate](#deactivate)
- [which python](#which-python)

---

# Kiểm tra
```bash
1. python --version | python3.10 --version      : Kiểm tra phiên bản python đang sử dụng.
2. python –m site | python –m site --user-site  : Hiển thị thông tin cài đặt python và các thư mục liên quan.
3. pip list                                     : kiểm tra tất cả các thư viện đã cài đặt.
4. pip show numpy                               : kiểm tra thư viện numpy đã cài vào máy chưa.
```

# Tạo môi trường ảo & activate
**Tạo và kích hoạt**
```bash
1. New terminal
2. python3 -m venv D:\python_env
3. D:\python_env\Scripts\activate (Windows) | source env/bin/activate (Linux)
```

# deactivate
Thoát khỏi môi trường ảo hiện tại.

# which python
```bash
- Xem đường dẫn môi trường run python trỏ đến đâu.
```

# Bài tập
## Demo bài tập 1
```python
from typing import List, Dict

def input_workers() -> List[Dict[str, str | float]]:
    list_workers = []

    n = int(input('Số lượng công nhân: '))

    for i in range(n):
        print(f'=== Nhập công nhân thứ {i+1} ===')
        worker_id = input('Mã công nhân: ')
        name = input('Họ tên công nhân: ')
        salary = float(input('Lương: '))
        days_work = float(input('Số ngày làm việc: '))
        allowance = float(input('Phụ cấp: '))

        worker = {
            'worker_id': worker_id,
            'name': name,
            'salary': salary,
            'days_work': days_work,
            'allowance': allowance
        }

        list_workers.append(worker)
    
    return list_workers

def print_table(data: List[Dict[str, str | float]]) -> None:
    headers = list(data[0].keys())

    col_widths = {
        h: max(len(h), max(len(str(row[h])) for row in data))
        for h in headers
    }

    headers_line = ' | '.join(f'{h:<{col_widths[h]}}' for h in headers)
    separator = '-+-'.join('-'*col_widths[h] for h in headers)

    print(headers_line)
    print(separator)

    for row in data:
        print(' | '.join(f'{str(row[h]):<{col_widths[h]}}' for h in headers))

def salary_calculation(list_workers: List[Dict[str, str | float]]):
    for i in range(len(list_workers)):
        row = list_workers[i]
        salary = row['salary']*row['days_work']
        list_workers[i]['sum_salary'] = salary

def sum_salary_max(list_workers: list):
    max_salary = 0

    for i in range(len(list_workers)):
        row = list_workers[i]
        if max_salary < row['sum_salary']:
            max_salary = row['sum_salary']

    list_max = []
    for i in range(len(list_workers)):
        row = list_workers[i]
        if row['sum_salary'] == max_salary:
            list_max.append(row)

    print('Số người có thu nhập nhiều nhất: ', len(list_max))
    print('=== Danh sách người có thu nhập lớn nhất ===')
    print_table(list_max)

def count_workers(list_workers):
    c = 0
    for i in range(len(list_workers)):
        row = list_workers[i]
        if row['salary'] != 0 and row['sum_salary'] > 15_000_000:
            c += 1
    
    print('Số lương công nhân không có thu nhập bằng 0 và tổng thu nhập lớn hơn 15 triệu là: ', c)

def main():
    list_workers = []

    print('=== Options ===')
    print('0. Thoát')
    print('1. Khởi tạo danh sách')
    print('2. Tính lương cơ bản')
    print('3. Số người có thu nhập lớn nhất')
    print('4. Số công nhận có thu nhập khác 0 và tổng thu nhập nhiều hơn 15 triệu')
    while True:
        option = int(input('Chọn options: '))

        if option == 0:
            break
        elif option == 1:
            list_workers = input_workers()
            print_table(list_workers)
        elif option == 2:
            salary_calculation(list_workers)
            print_table(list_workers)
        elif option == 3:
            sum_salary_max(list_workers)
        elif option == 4:
            count_workers(list_workers)
main()
```

## Bài tập 2
**Topic**
```bash
BÀI ÔN TẬP: QUẢN LÝ CÔNG NHÂN (KHÔNG DÙNG PANDAS)
Thuộc tính mỗi công nhân
- worker_id
- name
- salary (lương/ngày)
- days_work
- allowance
- sum_salary (tự tính)
Các nghiệp vụ có trong bài
✔ Khởi tạo danh sách (nhập)
✔ Thêm công nhân
✔ Sửa công nhân theo mã
✔ Xóa công nhân theo mã
✔ In bảng đẹp
✔ Tính tổng lương
✔ Lọc theo điều kiện
✔ Đếm theo điều kiện
✔ Sắp xếp
✔ Menu chuẩn đề thi
```
```python
from typing import List, Dict

# ===== NHẬP DANH SÁCH =====
def input_workers() -> List[Dict]:
    workers = []
    n = int(input("Số lượng công nhân: "))

    for i in range(n):
        print(f"--- Công nhân {i+1} ---")
        worker = {
            "worker_id": input("Mã: "),
            "name": input("Họ tên: "),
            "salary": float(input("Lương/ngày: ")),
            "days_work": int(input("Số ngày làm: ")),
            "allowance": float(input("Phụ cấp: "))
        }
        workers.append(worker)
    return workers


# ===== IN BẢNG =====
def print_table(data: List[Dict]):
    if not data:
        print("Danh sách rỗng")
        return

    headers = data[0].keys()
    widths = {h: max(len(h), max(len(str(r[h])) for r in data)) for h in headers}

    print(" | ".join(f"{h:<{widths[h]}}" for h in headers))
    print("-+-".join("-" * widths[h] for h in headers))

    for r in data:
        print(" | ".join(f"{str(r[h]):<{widths[h]}}" for h in headers))


# ===== TÍNH LƯƠNG =====
def calc_salary(workers: List[Dict]):
    for w in workers:
        w["sum_salary"] = w["salary"] * w["days_work"] + w["allowance"]


# ===== THÊM CÔNG NHÂN =====
def add_worker(workers: List[Dict]):
    worker = {
        "worker_id": input("Mã: "),
        "name": input("Họ tên: "),
        "salary": float(input("Lương/ngày: ")),
        "days_work": int(input("Số ngày làm: ")),
        "allowance": float(input("Phụ cấp: "))
    }
    workers.append(worker)


# ===== SỬA THEO MÃ =====
def update_worker(workers: List[Dict]):
    wid = input("Nhập mã cần sửa: ")
    for w in workers:
        if w["worker_id"] == wid:
            w["salary"] = float(input("Lương mới: "))
            w["days_work"] = int(input("Ngày làm mới: "))
            w["allowance"] = float(input("Phụ cấp mới: "))
            return
    print("Không tìm thấy!")


# ===== XÓA THEO MÃ =====
def delete_worker(workers: List[Dict]):
    wid = input("Nhập mã cần xóa: ")
    for i in range(len(workers)):
        if workers[i]["worker_id"] == wid:
            workers.pop(i)
            return
    print("Không tìm thấy!")


# ===== LỌC THU NHẬP > 15 TRIỆU =====
def filter_high_salary(workers: List[Dict]):
    result = []
    for w in workers:
        if w.get("sum_salary", 0) > 15_000_000:
            result.append(w)
    print_table(result)
    print("Số lượng:", len(result))


# ===== SẮP XẾP THEO LƯƠNG GIẢM DẦN =====
def sort_by_salary(workers: List[Dict]):
    workers.sort(key=lambda x: x.get("sum_salary", 0), reverse=True)


# ===== MENU =====
def main():
    workers = []

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
""")
        choice = int(input("Chọn: "))

        if choice == 0:
            break
        elif choice == 1:
            workers = input_workers()
        elif choice == 2:
            print_table(workers)
        elif choice == 3:
            calc_salary(workers)
        elif choice == 4:
            add_worker(workers)
        elif choice == 5:
            update_worker(workers)
        elif choice == 6:
            delete_worker(workers)
        elif choice == 7:
            filter_high_salary(workers)
        elif choice == 8:
            sort_by_salary(workers)
            print("Đã sắp xếp!")


main()
```