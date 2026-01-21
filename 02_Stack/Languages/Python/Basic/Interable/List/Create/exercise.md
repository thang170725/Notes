# Ép từ dict -> list of dict
**Ex1**
**Topic**
```bash
Cho một từ điển gồm có các khóa là mã sinh viên, các giá trị lưu trữ là điểm tổng kết. Hãy chuyển từ dạng dict -> list of dict
```
**Answer**
```python
scores = {
    "SV001": 8.5,
    "SV002": 7.0,
    "SV003": 9.25
}

result = [
    {"student_id": k, "score": v}
    for k, v in scores.items()
]

print(result) # [{'student_id': 'SV001', 'score': 8.5}, {'student_id': 'SV002', 'score': 7.0}, {'student_id': 'SV003', 'score': 9.25}]
```
Bài toán

Bạn có dict dạng:

data = {
    "SV001": [8.5, 7.0, 9.0],
    "SV002": [6.5, 7.5, 8.0],
    "SV003": [9.0, 9.5, 9.0]
}


Mỗi:

key = mã sinh viên

value = list điểm (hoặc dữ liệu liên quan)

👉 Muốn ép sang list of dict.

✅ Trường hợp 1 (PHỔ BIẾN NHẤT):
Value là list các cột (điểm, thuộc tính…)

Giả sử list có ý nghĩa:

[diem_toan, diem_ly, diem_hoa]

✨ Cách chuẩn & rõ ràng nhất
subjects = ["toan", "ly", "hoa"]

result = [
    {
        "mssv": k,
        **dict(zip(subjects, v))
    }
    for k, v in data.items()
]

📤 Kết quả
[
    {'mssv': 'SV001', 'toan': 8.5, 'ly': 7.0, 'hoa': 9.0},
    {'mssv': 'SV002', 'toan': 6.5, 'ly': 7.5, 'hoa': 8.0},
    {'mssv': 'SV003', 'toan': 9.0, 'ly': 9.5, 'hoa': 9.0}
]


✔ Chuẩn dữ liệu bảng
✔ In bảng đẹp, sort, filter dễ
✔ Tư duy giống pandas

**Ex3**
```python
data = {
    'msv': ['v1', 'v2'],
    'points': [2, 3]
}

result = [
    dict(zip(data.keys(), values))
    for values in zip(*data.values())
]

# [
#     {'msv': 'v1', 'points': 2},
#     {'msv': 'v2', 'points': 3}
# ]
```