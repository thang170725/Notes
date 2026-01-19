# @staticmethod
Đây là phương thức "độc lập" nhất. Nó không nhận self (đối tượng), cũng không nhận cls (lớp). Nó giống như một hàm bình thường nhưng được "nhốt" vào trong Class để dễ quản lý.
Đặc điểm: Không biết gì về các biến của lớp hay đối tượng.
Ứng dụng: Dùng cho các hàm tiện ích (utility) có logic liên quan đến Class nhưng không cần thay đổi gì trong Class đó.