- [Config (cấu hình)](#config-cấu-hình)
  - [python --version](#python---version)
  - [python –m site](#python-m-site)
  - [python –m site --user-site](#python-m-site---user-site)
  - [pip list](#pip-list)
  - [pip show](#pip-show)
  - [config env (môi trường ảo)](#config-env-môi-trường-ảo)
    - [deactivate](#deactivate)

# Kiểm tra
```bash
1. python --version | python3.10 --version      : Kiểm tra phiên bản python đang sử dụng.
2. python –m site | python –m site --user-site  : Hiển thị thông tin cài đặt python và các thư mục liên quan.
3. pip list                                     : kiểm tra tất cả các thư viện đã cài đặt.
4. pip show numpy                               : kiểm tra thư viện numpy đã cài vào máy chưa.
```

# Tạo môi trường ảo, activate & deactivate
**Tạo và kích hoạt**
```bash
1. New terminal
2. python3 -m venv D:\python_env
3. D:\python_env\Scripts\activate (Windows) | source env/bin/activate (Linux)
```
**Tắt bỏ**
# deactivate
Thoát khỏi môi trường ảo hiện tại.