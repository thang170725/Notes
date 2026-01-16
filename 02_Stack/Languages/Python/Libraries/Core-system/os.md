Os
    • Dùng để tương tác với hệ điều hành gồm: Làm việc với file và thư mục, Xử lý đường dẫn, Lấy thông tin môi trường (environment), chạy lệnh hệ thống
    • Không cần tải, cần import os
.getcwd()
Trả về đường dẫn hiện tại
Cú pháp:
print(os.getcwd())
.chdir()
Chuyển đến thư mục khác
Cú pháp:
os.chdir("C:/Users/Thang/Documents")
Listdir()
Liệt kê tên file/thư mục trong thư mục
Cú pháp:
print(os.listdir("."))
# liệt kê tất cả các file .txt trong thư mục
for filename in os.listdir("."):
    if filename.endswith(".txt"):
        print(filename)
# liệt kê tất cả file trong thư mục khác cùng cấp với thư mục cha
Mkdir()

makefirs()

rmdir()

removedirs()


Remove()
Rename()
Stat()
path
Join()
ghép đường dẫn đầy đủ tới ảnh “dataset/car/img1/jpg” chẳng hạn
Cú pháp:
img_path = os.path.join(input_folder, img_name)
Basename()
Dirname()
Lấy thư mục chứa file
Cú pháp:
print(os.path.dirname("/data/images/cat.jpg")) # /data/images
BASE_DIR = os.path.dirname(os.path.dirname(__file__)) 
print(__file__) # /home/thang/projects/tri_tue_nhan_tao/backend/visualizations/check_dataset.py (đường dẫn chạy file hiện tại)
print(BASE_DIR) # /home/thang/projects/tri_tue_nhan_tao/backend

exists
isfile
isdir
splitext()
relpath()
getenv
system()
name
sep
pathsep