id()
Để xem địa chỉ id của một biến trong bộ nhớ.
Cú pháp: id(<variable>)
Ép kiểu
Để ép từ một kiểu bất kỳ sang kiểu int (nếu ép được). Nếu biến cần ép không phải là số thì sẽ bị lỗi.
Cú pháp: int(<variable>)
a = "10"
b = int(a)
print(type(b))
<class 'int'>