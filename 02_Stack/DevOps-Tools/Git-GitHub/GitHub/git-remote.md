git remote
Dùng để kết nối môt repository git cục bộ (trên máy tính của bạn) với một repository từ xa (trên gitHub). giúp git push và git pull. Khi bạn khởi tạo một repository mới trên máy (git init), nó chưa biết liên kết với nơi nào để push code lên
Dùng khi bạn đã có sẵn code trên máy và muốn đẩy dự án này lên gitHub.
Cú pháp:
    1. git remote -v (Xem remote hiện tại là gì)
    2. git remote add origin https://github.com/thang1707/an_toan_bao_mat_tt.git
    3. git remote set-url origin https://github.com/thang170725/elgamal.git (Khi bạn muốn dùng remote origin nhưng trỏ tới repo mới)