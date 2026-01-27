- [clear](#clear)
- [tree](#tree)
- [du](#du)
- [free](#free)
- [df](#df)
---
# clear
```bash
Xóa hết các dòng lệnh.
```
# tree
xem cấu trúc thư mục hiện tại.
```bash
tree -L 10
```
# du
```bash
Xem dung lương thư mục hoặc file.
```
**Syn**
```bash
du -sh: xem dung lượng thư mục hiện tại
```
# free
Lệnh này cho bạn cái nhìn tổng quan nhất về dung lượng RAM tổng, dung lượng đã dùng, còn trống và bộ nhớ đệm (cache).
```bash
free -h
- -h: giúp hiển thị con số dưới dạng dễ đọc như GB, MB thay vì những dãy byte dài ngoằng
```

# df
Xem dung lượng còn lại của ổ, -h là để hiển thị theo đơn vị dễ đọc.
```bash
1. df -h /
2. df -h /home
```

