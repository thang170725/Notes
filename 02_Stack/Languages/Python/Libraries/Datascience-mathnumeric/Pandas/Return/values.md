.values[]
Để lấy giá trị ở một cột nào đó trong DataFrame.
File danhSach.csv có dữ liệu về height và weight.
dataFrame = pd.read_csv("danhSach.csv")
x = dataFrame.values[:, 0]
print(x)
[180 175 167 182 175 178 170 170 178 182 167 166 169 168 175 172]