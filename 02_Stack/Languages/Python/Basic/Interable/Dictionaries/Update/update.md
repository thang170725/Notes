update()
cập nhật phần tử với các mục từ đối số đã cho.
def main():
    di = {
        "name": "John",
        "age": 30,
        "address": "VietNam"
    }
    di.update({"age" : 40, "address": "USA"})
    print(di)
main()
{'name': 'John', 'age': 40, 'address': 'USA'}