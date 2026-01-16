- [read\_csv](#read_csv)
- [Series](#series)
- [DataFrame](#dataframe)
  - [.values](#values)
- [Tạo DataFrame mẫu](#tạo-dataframe-mẫu)
- [1️⃣ Phát hiện dòng trùng (toàn bộ cột)](#1️⃣-phát-hiện-dòng-trùng-toàn-bộ-cột)
- [2️⃣ Phát hiện trùng theo cột 'ID'](#2️⃣-phát-hiện-trùng-theo-cột-id)
- [3️⃣ Giữ dòng cuối cùng thay vì dòng đầu](#3️⃣-giữ-dòng-cuối-cùng-thay-vì-dòng-đầu)
- [4️⃣ Đánh dấu tất cả các dòng trùng](#4️⃣-đánh-dấu-tất-cả-các-dòng-trùng)
- [5️⃣ Lọc ra các dòng trùng](#5️⃣-lọc-ra-các-dòng-trùng)
- [Tạo DataFrame mẫu](#tạo-dataframe-mẫu-1)
- [1️⃣ Đếm số lần xuất hiện mỗi giá trị](#1️⃣-đếm-số-lần-xuất-hiện-mỗi-giá-trị)
- [có 125 hàng và 2 cột](#có-125-hàng-và-2-cột)
- [file csv này chỉ có 2 cột là text và intent](#file-csv-này-chỉ-có-2-cột-là-text-và-intent)
- [lấy ra 10 dòng dầu tiên](#lấy-ra-10-dòng-dầu-tiên)
- [tự động lấy ra 5 dòng đầu tiên (mặc địch)](#tự-động-lấy-ra-5-dòng-đầu-tiên-mặc-địch)
- [dữ liệu gốc dạng chuỗi](#dữ-liệu-gốc-dạng-chuỗi)
- [xóa cột age](#xóa-cột-age)
- [xóa hàng đầu tiên](#xóa-hàng-đầu-tiên)
- [change Array to Array dictionary](#change-array-to-array-dictionary)

---

```text
- Thường dùng để xử lý dữ liệu. Pandas kế thừa numpy tức là nó có thể sử dụng hầu hết các hàm trong numpy
- pip install pandas / conda install pandas.
```

# read_csv
Dùng để tải dữ liệu từ tệp CSV vào python.
**Syn**
```bash
li = pd.read_csv("danhSach.csv", index=[], encoding=’utf-8’) # dữ liệu hiển thị dưới dạng dataframe
```







.value_counts()
Đếm số lượng giá trị trong một cột.
Cú pháp:
c = self.df[column].value_counts()
df = pd.DataFrame({
    "Color": ["Red", "Blue", "Red", "Green", "Blue", "Yellow", "Red"]
})

# 1️⃣ Đếm số lần xuất hiện mỗi giá trị
print(df["Color"].value_counts())
Red       3
Blue      2
Green     1
Yellow    1
.nunique()
Để đếm tổng số lượng các giá trị khác nhau trong một cột nào đó.
Cú pháp:
df = pd.DataFrame({
    "Color": ["Red", "Blue", "Red", "Green", "Blue", "Yellow", "Red"]
})
print(df["Color"].nunique()) # 4
.apply()
self.df["length"] = self.df["text"].apply(lambda x: len(str(x).split())) # thêm cột độ dài câu
.str
Cú pháp:
import pandas as pd
df = pd.DataFrame({
    'text': ['  hello  ', '  world', 'chatgpt  ']
})
df['text'].str.strip() # phải thêm .str vào vì vế trước nó đang là series không phải chuỗi
.shape
Trả về số lượng hàng cột có trong dataFrame, …
print(df.shape)

(125, 2)
# có 125 hàng và 2 cột
.colums
Là một thuộc tính kiểu index. Nó chứa danh sách tên các cột của dataframe.
Cú pháp: df.columns
print(df.columns)

Index(['text', 'intent'], dtype='object')
# file csv này chỉ có 2 cột là text và intent
.values[]
Để lấy giá trị ở một cột nào đó trong DataFrame.
File danhSach.csv có dữ liệu về height và weight.
dataFrame = pd.read_csv("danhSach.csv")
x = dataFrame.values[:, 0]
print(x)
[180 175 167 182 175 178 170 170 178 182 167 166 169 168 175 172]
to_string()


iloc[]
print(li.iloc[0:2])



Read JSON
Các tập dữ liệu lớn thường được lưu trữ hoặc trích xuất dưới dạng JSON.
JSON là văn bản thuần túy, nhưng có định dạng của một đối tượng và rất phổ biến trong thế giới lập trình, bao gồm cả Pandas.
Xem ví dụ ở đây: https://www.w3schools.com/python/pandas/trypandas.asp?filename=demo_pandas_json

info()
