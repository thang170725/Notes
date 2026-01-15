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

# Series
Là mảng một chiểu giống như Numpy, hay là một cột của một bảng, nhưng nó thêm một cột đánh số thứ tự. Series có thể được khởi tạo thông qua Numpy, dict hoặc các dữ liệu vô hướng bình thường. Series có nhiều thuộc tính. Bạn có thể chuyển đổi Series sạng dạng dtype xác định, tạo bảng copy, trả về dạng bool của một thành phần.
**Ex**
```python
s = pd.Series([0,1,2,3], index=["a","b","c","d"])

# a    0
# b    1
# c    2
# d    3
# dtype: int64
```

# DataFrame
Là một cấu trúc dữ liệu 2 chiều hoặc nhiều chiều gồm các hàng, cột.
**Syn**
```bash
df = pd.DataFrame(data, index=None, columns=None, dtype=None, copy=False)
- data (dict, list, numpy array, …): Dữ liệu gốc tạo nên bảng.
- index (list hoặc array): Nhãn cho các dòng, mặc địn là 0,1,2, …
- columns (list hoặc array): Tên cho các cột (nếu không sẽ tự động lấy từ data).
- dtype: Ép kiểu dữ liệu cho toàn bộ bảng.
- copy (bool): Nếu True tạo bản sao của dữ liệu gốc.
```
**Ex**
```python
data = {
        "fullName": ["John", "Duo", "Chicago"],
        "address": ["New York", "Hanoi", "Tokyo"]
}
list = pd.DataFrame(data)
print(list)
   fullName   address
0     John  New York
1      Duo     Hanoi
2  Chicago     Tokyo
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
head()
    • Một trong những phương pháp được sử dụng nhiều nhất để có được cái nhìn tổng quan nhanh về DataFrame là phương pháp head().
    • head() trả về các tiêu đề và số lượng hàng được chỉ định, bắt đầu từ trên cùng hoặc lấy ra n dòng đầu tiên.
import pandas as pd

df = pd.read_csv('data.csv')
# lấy ra 10 dòng dầu tiên
print(df.head(10))
# tự động lấy ra 5 dòng đầu tiên (mặc địch)
print(df.head())
   Duration  Pulse  Maxpulse  Calories
0        60    110       130     409.1
1        60    117       145     479.0
2        60    103       135     340.0
3        45    109       175     282.4
4        45    117       148     406.0
5        60    102       127     300.5
6        60    110       136     374.0
7        45    104       134     253.3
8        30    109       133     195.1
9        60     98       124     269.0
   Duration  Pulse  Maxpulse  Calories
0        60    110       130     409.1
1        60    117       145     479.0
2        60    103       135     340.0
3        45    109       175     282.4
4        45    117       148     406.0
loc[]
Trả về một hoặc nhiều hàng được chỉ định.
import pandas as pd
def main():
    data = {
        "fullName": pd.Series(["John", "Jane", "Tom"]),
        "address": pd.Series(["New York", "HaNoi", "Tokyo"])
    }
    list = pd.DataFrame(data)
    print(list.loc[1])
    print(list)
main()
fullName     Jane
address     HaNoi
Name: 1, dtype: object
  fullName   address
0     John  New York
1     Jane     HaNoi
2      Tom     Tokyo
import pandas as pd
def main():
    data = {
        "fullName": pd.Series(["John", "Jane", "Tom"]),
        "address": pd.Series(["New York", "HaNoi", "Tokyo"])
    }
    list = pd.DataFrame(data)
    print(list.loc[[1,2]])
    print(list)
main()
  fullName address
1     Jane   HaNoi
2      Tom   Tokyo
  fullName   address
0     John  New York
1     Jane     HaNoi
2      Tom     Tokyo
iloc[]
print(li.iloc[0:2])

drop()
Là một phương thức dùng để xóa hàng (row) hoặc cột (column) khỏi DataFrame.
Cú pháp: DataFrame.drop(labels=None, axis=0, inplace=False)
    • labels: Tên hàng hoặc cột cần xóa.
    • axis: Xác định loại đối tượng cần xóa. 0 hoặc index – xóa theo hàng, 1 hoặc columns – xóa theo cột.
    • inplace: False (mặc định) trả về một bản sao mới của dataframe. True là thay đổi trực tiếp trên DataFrame gốc.
import pandas as pd
# dữ liệu gốc dạng chuỗi
df = pd.DataFrame(
{'name': ['Lan', 'Mai', 'Huy'],
 'age': [19, 20, 21]}
)
print("DataFrame ban đầu\n", df)
# xóa cột age
newDf = df.drop('age', axis=1)
print(newDf)
# xóa hàng đầu tiên
newDf1 = df.drop(0, axis=0)
print(newDf1)
DataFrame ban đầu
name  age
0  Lan   19
1  Mai   20
2  Huy   21
 name
0  Lan
1  Mai
2  Huy
name  age
1  Mai   20
2  Huy   21
pd.options.display.max_rows
Để kiểm tra số hàng tối đa của hệ thống.
import pandas as pd
def main():
    print(pd.options.display.max_rows)
main()
60
import pandas as pd
def main():
    pd.options.display.max_rows = 2
    data = {
        "fullName": ["John", "Jane", "Tom"],
        "address": ["New York", "HaNoi", "Tokyo"]
    }
    df = pd.DataFrame(data)
    print(pd.options.display.max_rows)
    print(df)
main()
2
   fullName   address
0      John  New York
..      ...       ...
2       Tom     Tokyo

[3 rows x 2 columns]
Read JSON
Các tập dữ liệu lớn thường được lưu trữ hoặc trích xuất dưới dạng JSON.
JSON là văn bản thuần túy, nhưng có định dạng của một đối tượng và rất phổ biến trong thế giới lập trình, bao gồm cả Pandas.
Xem ví dụ ở đây: https://www.w3schools.com/python/pandas/trypandas.asp?filename=demo_pandas_json
tail()
Để xem các hàng cuối cùng cùng của DataFrame. Trả về tiêu đề và số lượng hàng được chỉ định bắt đầu từ dưới cùng.
info()
Ví dụ
Tạo danh sách quản lý sinh viên bằng pandas
                                   name  age   gender      address      gpa
0                   Le Duc Thang    20      male       Ha Noi    3.09
1 Nguyen Dang Nhat Minh     20      male  Thai Binh    3.00
2                Nguyen Van Tai     20      male       Ha Noi    3.09
3             Nguyen Minh Thu    20   female    Bac Ninh    2.89
4                   Le Nhu Quỳnh    20      male           Ba vi    3.10
import pandas as pd
class student():
    def __init__(self, name, age, gender, address, gpa):
        self.name = name
        self.age = age
        self.gender = gender
        self.address = address
        self.gpa = gpa

# change Array to Array dictionary
def addList(li, students):
    for student in students:
        data = {
            "name": student.name,
            "age": student.age,
            "gender": student.gender,
            "address": student.address,
            "gpa": student.gpa
        }
        li.append(data)
def main():
    student1 = student("Le Duc Thang", 20, "male", "Ha Noi", 3.09)
    student2 = student("Nguyen Dang Nhat Minh", 20, "male", "Thai Binh", 3)
    student3 = student("Nguyen Van Tai", 20, "male", "Ha Noi", 3.09)
    student4 = student("Nguyen Minh Thu", 20, "female", "Bac Ninh", 2.89)
    student5 = student("Le Nhu Quỳnh", 20, "male", "Ba vi", 3.1)

    li = []
    students = [student1, student2, student3, student4, student5]
    addList(li, students)

    listStudent = pd.DataFrame(li)
    print(listStudent)
main()

