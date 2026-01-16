# create database
```bash
- Dùng để tạo database.
```
**Syn**
```sql
create database MyDatabase  -- Tạo một database
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci; -- Như vậy mặc định schema MyDatabase sẽ dùng utf8mb4 + utf8mb4_unicode_ci
```

# Use
```bash
Dùng để chọn database.
```
**Syn**
```sql
use MyDatabase;
```