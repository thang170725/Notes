```text
tạo DockerFile và chạy thử Docker container
```

# 1. Cài Docker
```text
Trước hết, phải chắc chắn Docker đã được cài trên máy.
```
```bash
docker --version
docker compose version
```
**Nếu chưa cài, bạn có thể dùng trên Ubuntu**
```bash
sudo apt update
sudo apt install docker.io docker-compose -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER  # để chạy docker không cần sudo
```
Sau đó đăng xuất rồi đăng nhập lại để quyền có hiệu lực.

# 2. Tạo thư mục dự án
Tạo một thư mục mới, ví dụ mydockerapp:
```bash
mkdir mydockerapp
cd mydockerapp
```

# 3. Tạo file Python đơn giản
Tạo app.py:
```python
# app.py
print("Hello from Docker!")
```

# 4. Tạo Dockerfile
Tạo một file tên Dockerfile (không có đuôi):
```Dockerfile
# Dockerfile
# Sử dụng image Python chính thức
FROM python:3.12-slim

# Thiết lập thư mục làm việc trong container
WORKDIR /app

# Copy file Python vào container
COPY app.py .

# Lệnh để chạy khi container start
CMD ["python", "app.py"]

Giải thích nhanh:

FROM python:3.12-slim → dùng image Python 3.12 nhẹ.

WORKDIR /app → thư mục làm việc trong container.

COPY app.py . → copy file app.py vào container.

CMD ["python", "app.py"] → chạy lệnh khi container khởi động.
```

# 5. Build Docker image
Chạy lệnh này trong thư mục chứa Dockerfile:

docker build -t mypythonapp .


-t mypythonapp → đặt tên cho image là mypythonapp.

. → Dockerfile ở thư mục hiện tại.

Docker sẽ đọc Dockerfile và tạo image.

# 6. Chạy Docker container
docker run --name testapp mypythonapp


Kết quả bạn sẽ thấy:

Hello from Docker!


Nếu muốn container chạy trong background:

docker run -d --name testapp mypythonapp


-d → detached mode (chạy ngầm).

# 7. Kiểm tra container
docker ps -a   # liệt kê tất cả container
docker logs testapp  # xem log của container

# 8. Xóa container & image
docker stop testapp
docker rm testapp
docker rmi mypythonapp