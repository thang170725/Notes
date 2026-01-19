Xử lý điều kiện
If … else
Tìm kiếm 1 phần tử có nằm trong một mảng hay không:
a = ["VietNam", "America", "Island", "Porland", "Canada"]
if "ThaiLand" in a: # kiểm tra xem ThaiLand có xuất hiện trong mảng không
    print("True")
else:
    print("False")
False
Kiểm tra xem mảng có phần tử nào không:
a = ["VietNam", "America", "Island", "Porland", "Canada"]
if a:
    print("is not Empty")
else:
    print("is Empty")
is not Empty
# mảng a đang có 5 phần từ nên in ra “is not Empty”
Gán giá trị với một điều kiện nào đó:
a = ""
if len(a) != 0:
    a = "not empty"
else:
    a = "is empty"
print(a)
is empty
a = ""
a = "not empty" if(len(a) != 0) else "is empty"
print(a)
is empty
pass
Câu lệnh if elif hay else không được để trống nhưng vì một lý do nào đó muốn để trống thì thêm pass vào để tránh gặp lỗi.
a = 33
b = 200
if b > a:
  pass

Short Hand If … else
a = ["VietNam", "America", "Island", "Porland", "Canada"]
print(True) if "ThaiLand" in a else print("False")
False
