intersection_update()
Chỉ giữ lại các phần tử trùng lặp, nhưng nó sẽ thay đổi tập hợp gốc thay vì trả về tập hợp mới.
Cú pháp: <variable1>.intersection_update(<variable2>)
mySet= {"apple", "banana", "orange", "Lemon"}
orther = {"orange", "Lemon", "Passion"}
mySet.intersection_update(orther)
print(mySet)
{'orange', 'Lemon'}
