- [if … else](#if--else)
- [Short Hand If … else](#short-hand-if--else)

---

# if … else
**Ex1: Tìm kiếm 1 phần tử có nằm trong một mảng hay không**
```bash
a = ["VietNam", "America", "Island", "Porland", "Canada"]

if "ThaiLand" in a: # kiểm tra xem ThaiLand có xuất hiện trong mảng không
    print("True")
else:
    print("False")

# False
```
**Ex2: Kiểm tra xem mảng có phần tử nào không**
```python
a = ["VietNam", "America", "Island", "Porland", "Canada"]

if a:
    print("is not Empty")
else:
    print("is Empty")

# is not Empty
# mảng a đang có 5 phần từ nên in ra “is not Empty”
```

# Short Hand If … else
**Ex**
```python
a = ["VietNam", "America", "Island", "Porland", "Canada"]
print(True) if "ThaiLand" in a else print("False") # False
```