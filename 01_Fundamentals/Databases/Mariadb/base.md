```bash
- MariaDB là một hệ quản trị CSDL RIÊNG BIỆT. Không phải “chế độ” của MySQL
- MySQL ban đầu do Monty Widenius tạo. Oracle mua MySQL. Monty fork MySQL → tạo MariaDB. MariaDB = con ruột của MySQL gốc
```
**Vì sao query giống MySQL gần như 100%?**
```bash
- MariaDB giữ tương thích ngược MySQL
- Cùng SQL dialect
- Cùng protocol
- Cùng port 3306
```

# Cách tạo db
```bash
1.  sudo mariadb
2.  CREATE USER 'ai_user'@'localhost' IDENTIFIED BY 'ai123';
3.
    GRANT ALL PRIVILEGES ON house_price_project.* TO 'ai_user'@'localhost';
    FLUSH PRIVILEGES;
4.  SELECT user, host FROM mysql.user;
5.  EXIT;
6.  mariadb -u ai_user -p
```
