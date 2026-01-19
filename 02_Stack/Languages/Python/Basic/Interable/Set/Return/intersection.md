intersection()
Trả về một set mới chỉ chứa các phần tử có trong cả 2 set cũ.
Cú pháp: <variable1>.intersection(<variable2>)
mySet= {"apple", "banana", "orange", "Lemon"}
orther = {"orange", "Lemon", "Passion"}
Set = mySet.intersection(orther)
print(Set)
{'Lemon', 'orange'}
mySet= {"apple", "banana", "orange", "Lemon"}
orther = {"orange", "Lemon", "Passion"}
Set = mySet & orther
print(Set)
{'Lemon', 'orange'}