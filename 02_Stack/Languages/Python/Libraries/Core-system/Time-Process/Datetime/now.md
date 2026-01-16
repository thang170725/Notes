```bash
Lấy ngày + giờ hiện tại.
```
```python
now = datetime.now()
print(now)

# 2026-01-12 18:35:10.123456
```

# Truy cập từng thành phần ngày giờ
```python
now = datetime.now()

print(now.year)    # năm
print(now.month)   # tháng
print(now.day)     # ngày
print(now.hour)    # giờ
print(now.minute)  # phút
print(now.second)  # giây
```