    • Docker tạo container (tức gói ứng dụng cùng môi trường (code, thư viện, runtime) vào một đơn vị nhẹ, có thể chạy trên bất kỳ máy nào có Docker. Container nhẹ hơn máy ảo, khởi động nhanh và dễ tái tạo môi trường.
    • Tại sao dùng: tránh “works on my machine”, dễ đóng gói app + dependency, deploy, test, chia sẻ với đồng đội, CI/CD, scale.
    • Rất phổ biến trong devops, backend, data science, ML engineering. Công ty/startup đều dùng rộng rãi. Với intern AI / trình độ hiện tại: RẤT NÊN học. Kiến thức cơ bản Docker giúp bạn:
    • Chạy service phức tạp (MQTT, DB, backend, frontend) trên máy dev chỉ bằng vài lệnh.
    • Đóng gói model/serving để deploy. Giảm thời gian setup môi trường khi chia sẻ project với bạn bè/đồng nghiệp.
Cách cài đặt
Ubuntu:
# 1. Cập nhật và cài phụ thuộc
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release

# 2. Thêm khoá GPG của Docker
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# 3. Thêm repository chính thức (Ubuntu 24.04 -> 'lunar' hoặc apt will auto-resolve; chung cấu hình)
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 4. Cập nhật và cài Docker Engine + CLI + containerd + compose plugin
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# 5. Kích hoạt và khởi động docker
sudo systemctl enable --now docker

# 6. (Tùy chọn) cho phép user hiện tại chạy docker không cần sudo
sudo usermod -aG docker $USER

# Đăng xuất / đăng nhập lại hoặc chạy `newgrp docker` để thay đổi nhóm có hiệu lực.
newgrp docker

docker run --rm hello-world
docker run
docker run -it ubuntu bash (bạn sẽ thấy prompt bị đổi thành kiểu: root@c2a17d31f42f:/#)
    • dodocker run → tạo container mới và chạy
    • -it → interactive + gắn terminal
    • ubuntu → tên image (Docker tự tải nếu máy bạn chưa có)
    • bash → lệnh chạy khi container khởi độngcker run -it ubuntu bash
docker images
Xem image đang có trong máy
docker ps
Cú pháp:
docker ps
docker ps -a (Xem container đã dừng)
docker rm
Xóa theo Id
Cú pháp:
docker rm <container_id>
docker rmi
Xóa image
Cú pháp:
docker rmi ubuntu
docker stop

docker container prune
Xóa tất cả container đã dừng

Exit
Thoát khỏi docker
