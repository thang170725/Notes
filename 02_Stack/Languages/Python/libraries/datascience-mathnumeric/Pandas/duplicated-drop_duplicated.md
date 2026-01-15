# .duplicated()
```bash
- Để phát hiện dòng trùng lặp trong DataFrame.
```
**Syn**
```bash
DataFrame.duplicated(subset=None, keep='first')
- subset: (tùy chọn) — cột hoặc danh sách cột để kiểm tra trùng (mặc định kiểm tất cả cột)
- keep:
    + 'first': đánh dấu True từ dòng trùng thứ 2 trở đi
    + 'last': đánh dấu True trừ dòng cuối cùng
    + False: tất cả các dòng trùng đều được đánh dấu T
```
**Ex**
```python
import pandas as pd

# Tạo DataFrame mẫu
df = pd.DataFrame({
    'ID': [1, 2, 2, 3, 4, 4, 4, 5],
    'Name': ['An', 'Bình', 'Bình', 'Cường', 'Dũng', 'Dũng', 'Dũng', 'Hà']
})

print("=== Dataset gốc ===")
print(df)

# 1️⃣ Phát hiện dòng trùng (toàn bộ cột)
print("\nDuplicated toàn bộ cột:")
print(df.duplicated())

# 2️⃣ Phát hiện trùng theo cột 'ID'
print("\nDuplicated theo cột ID:")
print(df.duplicated(subset='ID'))

# 3️⃣ Giữ dòng cuối cùng thay vì dòng đầu
print("\nDuplicated (keep='last'):")
print(df.duplicated(subset='ID', keep='last'))

# 4️⃣ Đánh dấu tất cả các dòng trùng
print("\nDuplicated (keep=False):")
print(df.duplicated(subset='ID', keep=False))

# 5️⃣ Lọc ra các dòng trùng
print("\nCác dòng trùng lặp:")
print(df[df.duplicated(subset='ID', keep=False)])
.drop_duplicates()
Để xóa dòng trùng.
Cú pháp:
df_no_dup = df.drop_duplicates(subset='ID', keep='first')
import pandas as pd
```

# drop_duplicates()
**Ex**
```python
# Tạo DataFrame mẫu
df = pd.DataFrame({
    'ID': [1, 2, 2, 3, 4, 4, 4, 5],
    'Name': ['An', 'Bình', 'Bình', 'Cường', 'Dũng', 'Dũng', 'Dũng', 'Hà']
})

df = df.drop_duplicates(subset=['ID'], keep='first')
print(df)

#    ID   Name
# 0   1     An
# 1   2   Bình
# 3   3  Cường
# 4   4   Dũng
# 7   5     Hà
```