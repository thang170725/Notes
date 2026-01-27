- [Hóa Đơn bán hàng](#hóa-đơn-bán-hàng)
---
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
```python
from typing import Protocol

class Tax(Protocol):
    def tax(self):
        ...

class Tivi:
    def __init__(self, name, price, quantity):
        self.name = name
        self.price = price
        self.quantity = quantity
        self.t = self.tax()
        self.total = self.total_item
        
    
    @property
    def total_item(self):
        total = self.price * self.quantity * self.t
        return total
    
    def tax(self):
        self.t = 0.5
        return self.t

class Fan:
    def __init__(self, name, price, quantity):
        self.name = name
        self.price = price
        self.quantity = quantity
        self.t = self.tax()
        self.total = self.total_item
        
    
    @property
    def total_item(self):
        total = self.price * self.quantity * self.t
        return total
    
    def tax(self):
        self.t = 0.6
        return self.t

class Mobi:
    def __init__(self, name, price, quantity):
        self.name = name
        self.price = price
        self.quantity = quantity
        self.t = self.tax()
        self.total = self.total_item
        
    
    @property
    def total_item(self):
        total = self.price * self.quantity * self.t
        return total
    
    def tax(self):
        self.t = 0.7
        return self.t

class Item:
    def __init__(self, name, price, quantity, value):
        self.name = name
        self.price = price
        self.quantity = quantity
        self.t = self.tax(value)
        self.total = self.total_item
    
    @property
    def total_item(self):
        total = self.price * self.quantity * self.t
        return total
    
    def tax(self, value):
        self.t = value
        return self.t
        
class Items:
    def __init__(self):
        self.items = []
    
    def add_item(self, item: Item):
        self.items.append(item)
    
    def sum_total(self):
        sum_items = 0
        for item in self.items:
            sum_items += item.total
            
        return sum_items

class GoodsReceipt:
    def __init__(self, id_receipt, id_brand, address, days, name_brand):
        self.id_receipt = id_receipt
        self.id_brand = id_brand
        self.address = address
        self.days = days
        self.name_brand = name_brand


        self.items = Items()
    
    def print_receipt(self):
        print('\nPHIẾU NHẬP HÀNG')
        print("-" * 56)

        print(f"Mã phiếu: {self.id_receipt} {' '*20} Ngày lập: {self.days}")
        print(f"Mã NCC: {self.id_brand} {' '*20} Tên NCC: {self.name_brand}")
        print(f"Địa chỉ: {self.address}")
        print("-" * 56)

        print(f"{'Tên hàng':<15} | {'Đơn giá':>6} | {'Số lượng':>12} | {'Thành tiền':>15}")
        print("-" * 56)

        for i in self.items.items:
            print(f"{i.name:<15} | {i.price:>6} | {i.quantity:>12.2f} | {i.total:>15.2f}")

        print("-"*56)
        print("Tổng tiền:", self.items.sum_total())

def tax_item(t: Tax):
    print(t.tax())

if __name__ == "__main__":
    tivi = Tivi('TiVi', 30, 2)
    fan = Fan("Quạt", 1.2, 3)
    mobi = Mobi("Mobi", 5, 10)
    
    tax_item(tivi)
    tax_item(fan)
    tax_item(mobi)
    
    li = [tivi, fan, mobi]
    
    receipt = GoodsReceipt('PH001', 'NCC1', "Khu công nghiệp Như Quỳnh A", '1/1/2007', 'LG-Electronic')
    for item in li:
        receipt.items.add_item(item)
    
    receipt.print_receipt()
```