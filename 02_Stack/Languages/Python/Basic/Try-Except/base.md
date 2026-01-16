Try…Except
Được dung để bắt và xử lý lỗi (exception) khi chạy chương trình, tránh chương trình bị “crash” bất ngờ.
Cú pháp:
try:
    # đoạn code có thể gây lỗi
    nguy_hiem = 10 / 0  # lỗi chia cho 0
except:
    # xử lý khi có lỗi
    print("Đã xảy ra lỗi!")
FileNotFoundError
Lỗi không tìm thấy file.
try:
    # code có thể lỗi
    f = open("file_khong_ton_tai.txt", "r")
except FileNotFoundError:
    print("Không tìm thấy file!")

ZeroDivisisionError
Lỗi chia cho không.

except ZeroDivisionError:
    print("Không được chia cho 0!")

Bắt mọi loại lỗi và xem nội dung lỗi
try:
    result = 10 / 0
except Exception as e:
    print("Có lỗi xảy ra:", e)

