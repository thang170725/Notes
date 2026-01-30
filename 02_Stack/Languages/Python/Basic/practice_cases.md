- [Quản lý sự kiện](#quản-lý-sự-kiện)
- [Hóa Đơn bán hàng](#hóa-đơn-bán-hàng)
- [Quản lý phiếu nhập hàng](#quản-lý-phiếu-nhập-hàng)
---
# Quản lý sự kiện
```bash
1. Tạo danh sách n phần tử (n>=5). Mỗi sự kiện là 1 dict gồm mã, tên, địa điểm, ngày, số người.
2. Viết hàm thêm chi phí nếu chưa có.
3. Tính chi phí trung bình.
4. sắp xếp theo số người tham gia.
5. tìm và in ra sự kiện có người tham gia đông nhất.
6. chương trình chính nhập -> thêm -> sắp xếp -> tìm -> in.
```
```python
def create_event():
    while True:
        n = int(input('n = '))
        if n >= 5:
            break

    return [{
            'id': input("id = "),
            'name': input("name = "),
            'address': input("address = "),
            'day': input("day = "),
            'people': int(input("people = "))
        }
        for _ in range(n)
    ]

def add_column(events: list, key="cost"):
    for row in events:
        if key not in row.keys():
            row[key] = float(input("cost = "))

def mean_cost(events: list):
    return sum(row['cost'] for row in events)/len(events)

def sort_event(events: list):
    events.sort(key=lambda row : row['people'])

def find_max(events: list):
    m = max(row['people'] for row in events)

    return [row for row in events if row['people'] == m]

def main():
    events = create_event()
    add_column(events)
    print(mean_cost(events))
    sort_event(events)
    print(events)
    print(find_max(events))
main()
```
# Hóa Đơn bán hàng
```python
from datetime import date

class Item:
    def __init__(self, name, quantity, price):
        self.name = name
        self.quantity = quantity
        self.price = price
        self.total = quantity * price

class ItemList:
    def __init__(self):
        self.items = []
        
    def input_items(self):
        n = int(input('Số mặt hàng: '))
        for _ in range(n):
            name = input('Tên hàng: ')
            qty = int(input('Số lượng: '))
            price = float(input('Đơn giá: '))

            self.items.append(Item(name, qty, price))
    
    def sum_quantity(self):
        return sum(i.quantity for i in self.items)

    def sum_price(self):
        return sum(i.price for i in self.items)

    def sum_total(self):
        return sum(i.total for i in self.items)

    def total_row(self):
        return {
            "name": "CỘNG",
            "quantity": self.sum_quantity(),
            "price": self.sum_price(),
            "total": self.sum_total()
        }
    
class Store:
    def __init__(self, name, address, phone):
        self.name = name
        self.address = address
        self.phone = phone

class Customer:
    def __init__(self):
        self.name = input('Tên khách hàng: ')
        self.address = input('Địa chỉ khách hàng: ')

class SalesInvoice:
    def __init__(self):
        self.store = Store(
            'Đức Thắng Market',
            'Phú Đa - Hoài Đức - Hà Nội',
            '0123456789'
        )

        self.customer = Customer()
        self.item_list = ItemList()
        self.item_list.input_items()

        self.date= date.today()
        self.staff = 'Lê Đức Thắng'
    
    def print_invoice(self):
        print('\nHÓA ĐƠN BÁN HÀNG')
        print("-" * 56)

        print(self.store.name)
        print('Địa chỉ: ', self.store.address)
        print('ĐT: ', self.store.phone)
        print("-" * 56)

        print('Tên khách hàng: ', self.customer.name)
        print('Địa chỉ: ', self.customer.address)
        print("-" * 56)

        print(f"{'Tên hàng':<15} | {'SL':>6} | {'Đơn giá':>12} | {'Thành tiền':>15}")
        print("-" * 56)

        for i in self.item_list.items:
            print(f"{i.name:<15} | {i.quantity:>6} | {i.price:>12.2f} | {i.total:>15.2f}")

        print("-"*40)
        print("Tổng tiền:", self.item_list.sum_total())
        print(self.date, "|", self.staff)
       
    def _box_line(self, text="", width=70):
        print("| " + text.ljust(width - 4) + " |")

    def print_invoice_box(self):
        WIDTH = 70

        print("+" + "-"*(WIDTH-2) + "+")
        self._box_line("HÓA ĐƠN BÁN HÀNG", WIDTH)
        print("+" + "-"*(WIDTH-2) + "+")

        self._box_line(self.store.name, WIDTH)
        self._box_line(f"Địa chỉ: {self.store.address}", WIDTH)
        self._box_line(f"ĐT: {self.store.phone}", WIDTH)

        print("+" + "-"*(WIDTH-2) + "+")

        self._box_line(f"Tên khách hàng: {self.customer.name}", WIDTH)
        self._box_line(f"Địa chỉ: {self.customer.address}", WIDTH)

        print("+" + "-"*(WIDTH-2) + "+")

        # Header bảng
        header = (
            f"{'STT':>3} | {'Tên hàng':<15} | {'SL':>6} | "
            f"{'Đơn giá':>12} | {'Thành tiền':>15}"
        )
        self._box_line(header, WIDTH)
        self._box_line("-"*66, WIDTH)

        # Dữ liệu bảng
        for idx, i in enumerate(self.item_list.items, start=1):
            row = (
                f"{idx:>3} | {i.name:<15} | {i.quantity:>6} | "
                f"{i.price:>12.2f} | {i.total:>15.2f}"
            )
            self._box_line(row, WIDTH)
        
        self._box_line("-"*66, WIDTH)

        t = self.item_list.total_row()
        total_row = (
            f"{'':>3} | {t['name']:<15} | {t['quantity']:>6} | "
            f"{t['price']:>12.2f} | {t['total']:>15.2f}"
        )
        self._box_line(total_row, WIDTH)

        print("+" + "-"*(WIDTH-2) + "+")

        self._box_line(f"Tổng tiền: {self.item_list.sum_total():.2f}", WIDTH)
        self._box_line(f"{self.date} | {self.staff}", WIDTH)

        print("+" + "-"*(WIDTH-2) + "+")


if __name__ == "__main__":
    invoice = SalesInvoice()
    invoice.print_invoice_box()
```
# Quản lý phiếu nhập hàng
**Duck typing**
```python
from typing import Protocol

class Tax(Protocol):
    def tax(self):
        pass

class Item:
    def __init__(self, name, price, quantity):
        self.name = name
        self.price = price
        self.quantity = quantity
        self.t = self.tax()
        self.total = self.total_item
    
    @property
    def total_item(self):
        return self.price * self.quantity * self.t
    
    def tax(self):
        return 1.0

class Tivi(Item):
    def tax(self):
        return 0.5

class Fan(Item):
    def tax(self):
        return 0.6

class Mobi(Item):
    def tax(self):
        return 0.7
        
class Items:
    def __init__(self):
        self.items = []
    
    def add_item(self, item: Item):
        self.items.append(item)
    
    def sum_total(self):    
        return sum(i.total for i in self.items)

class GoodsReceipt:
    def __init__(self, id_receipt, id_brand, address, date, name_brand):
        self.id_receipt = id_receipt
        self.id_brand = id_brand
        self.address = address
        self.date = date
        self.name_brand = name_brand
        self.items = Items()
    
    def print_receipt(self):
        print('\nPHIẾU NHẬP HÀNG')
        print("-" * 56)

        print(f"Mã phiếu: {self.id_receipt} {' '*20} Ngày lập: {self.date}")
        print(f"Mã NCC: {self.id_brand} {' '*20} Tên NCC: {self.name_brand}")
        print(f"Địa chỉ: {self.address}")
        print("-" * 56)

        print(f"{'Tên hàng':<15} | {'Đơn giá':>6} | {'Số lượng':>12} | {'Thành tiền':>15}")
        print("-" * 56)

        for i in self.items.items:
            print(f"{i.name:<15} | {i.price:>6} | {i.quantity:>12.2f} | {i.total:>15.2f}")

        print("-"*56)
        print("Tổng tiền:", self.items.sum_total())

def print_tax(t: Tax):
    print(t.tax())

if __name__ == "__main__":
    tivi = Tivi('TiVi', 30, 2)
    fan = Fan("Quạt", 1.2, 3)
    mobi = Mobi("Mobi", 5, 10)
    li = [tivi, fan, mobi]

    print_tax(tivi)
    print_tax(fan)
    print_tax(mobi)   
    
    receipt = GoodsReceipt(
        'PH001', 
        'NCC1', 
        "Khu công nghiệp Như Quỳnh A", 
        '1/1/2007', 
        'LG-Electronic'
    )

    for item in li:
        receipt.items.add_item(item)
    
    receipt.print_receipt()
```
**Truyền thống**
```python
from abc import ABC, abstractmethod

class Item(ABC):
    def __init__(self, name, price, quantity):
        self.name = name
        self.price = price
        self.quantity = quantity
        self.t = self.tax()
        self.total = self.total_item

    @abstractmethod
    def tax(self):
        pass

    @property
    def total_item(self):
        return self.price * self.quantity * self.t
    
class Tivi(Item):
    def tax(self):
        return 0.5

class Fan(Item):
    def tax(self):
        return 0.6

class Mobi(Item):
    def tax(self):
        return 0.7

class Items:
    def __init__(self):
        self.items = []

    def add_item(self, item: Item):
        self.items.append(item)

    def sum_total(self):
        return sum(i.total for i in self.items)

class GoodsReceipt:
    def __init__(self, id_receipt, id_brand, address, date, name_brand):
        self.id_receipt = id_receipt
        self.id_brand = id_brand
        self.address = address
        self.date = date
        self.name_brand = name_brand
        self.items = Items()

    def print_receipt(self):
        print("\nPHIẾU NHẬP HÀNG")
        print("-" * 56)

        print(f"Mã phiếu: {self.id_receipt} {' '*20} Ngày lập: {self.date}")
        print(f"Mã NCC: {self.id_brand} {' '*20} Tên NCC: {self.name_brand}")
        print(f"Địa chỉ: {self.address}")
        print("-" * 56)

        print(f"{'Tên hàng':<15} | {'Đơn giá':>6} | {'Số lượng':>12} | {'Thành tiền':>15}")
        print("-" * 56)

        for i in self.items.items:
            print(f"{i.name:<15} | {i.price:>6} | {i.quantity:>12.2f} | {i.total:>15.2f}")

        print("-" * 56)
        print("Tổng tiền:", self.items.sum_total())

def print_tax(item: Item):
    print(item.tax())

if __name__ == "__main__":
    tivi = Tivi("TiVi", 30, 2)
    fan = Fan("Quạt", 1.2, 3)
    mobi = Mobi("Mobi", 5, 10)

    print_tax(tivi)
    print_tax(fan)
    print_tax(mobi)

    receipt = GoodsReceipt(
        "PH001",
        "NCC1",
        "Khu công nghiệp Như Quỳnh A",
        "1/1/2007",
        "LG-Electronic"
    )

    receipt.items.add_item(tivi)
    receipt.items.add_item(fan)
    receipt.items.add_item(mobi)

    receipt.print_receipt()
```