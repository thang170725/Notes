# sudo apt clean
Xóa toàn bộ file .deb đã tải

sudo apt autoclean
Chỉ xóa các gói cũ, không còn dùng.

2️⃣ Xóa package không còn cần thiết
bash
Copy code
sudo apt autoremove
Xóa dependency thừa sau khi gỡ phần mềm.

👉 Thường nên chạy combo:

bash
Copy code
sudo apt autoremove --purge
sudo apt clean
3️⃣ Dọn log hệ thống (journal)
Kiểm tra log đang chiếm bao nhiêu:

bash
Copy code
journalctl --disk-usage
Chỉ giữ log 7 ngày:

bash
Copy code
sudo journalctl --vacuum-time=7d
Hoặc giới hạn dung lượng (ví dụ 500MB):

bash
Copy code
sudo journalctl --vacuum-size=500M
4️⃣ Dọn cache người dùng
bash
Copy code
rm -rf ~/.cache/*
⚠️ Lệnh này chỉ xóa cache, không ảnh hưởng dữ liệu cá nhân.

5️⃣ Nếu có dùng Docker (rất hay đầy disk)
Kiểm tra:

bash
Copy code
docker system df
Dọn rác Docker:

bash
Copy code
docker system prune -a
⚠️ Sẽ xóa image, container không dùng.

6️⃣ Nếu dùng Snap
Xem snap chiếm dung lượng:

bash
Copy code
du -h /var/lib/snapd/snaps | sort -h
Xóa snap version cũ:

bash
Copy code
sudo snap set system refresh.retain=2
sudo snap remove --purge <tên_snap>
7️⃣ Tìm thư mục “ăn dung lượng”
Rất hữu ích:

bash
Copy code
sudo du -h / --max-depth=1 2>/dev/null | sort -h
Hoặc dùng công cụ trực quan:

bash
Copy code
sudo apt install ncdu
sudo ncdu /
👉 Gợi ý nhanh
Nếu bạn chỉ muốn dọn rác cơ bản, an toàn, cứ chạy:

bash
Copy code
sudo apt autoremove --purge
sudo apt clean
sudo journalctl --vacuum-time=7d