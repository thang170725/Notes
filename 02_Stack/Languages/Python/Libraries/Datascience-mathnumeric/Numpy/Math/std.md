Std()
Là độ lệnh chuẩn tổng thể
Ví dụ:
Tính độ lệch chuẩn tổng thể và độ lệch chuẩn mẫu của 5 số 12,34,45,70,86
    1) Tính trung bình cộng: (12 + 34 + 45 + 70 + 86) / 5 = 49.4 
    2) Tính phương sai mẫu: ((12-49.4)**2 + (34-49.4)**2 + (45-49.4)**2 + …) / (5-1) = 854.8 
Tính phương sai tổng thể: ((12-49.4)**2 + (34-49.4)**2 + (45-49.4)**2 + …) / 5 = 683.84  
    1) Tính độ lệch chuẩn của phương sai mẫu: np.sqrt(854.8)= 29.23696291
       Tính độ lệch chuẩn của phương sai tổng thể: np.sqrt(683.84) = 26.15 
Cú pháp:
value = [12,34,45,70,86]    
print(np.std(value)) # trả về độ lệch chuẩn tổng thế
26.150334605889842
Exp()