4. AI
Math (Toán học)
Đạo hàm
Đạo hàm là “tốc độ thay đổi” của một đại lượng.
    • Tối ưu hóa: Tìm điểm nhỏ nhất, lớn nhất trong hàm (mất mát trong ML).
    • Kinh tế: Tối đa hóa lợi nhuận, tối thiểu hóa chi phí.
    • Vật lý: Mối liên hệ giữa vị trí - vận tốc - gia tốc.
    • ML/DL: Sử dụng tính toán hàm mất mát (gradient descent).Nếu không có đạo hàm → máy không biết “học” thế nào để tốt hơn.
    • Game: Mô phỏng chuyển động, ánh sáng, âm thanh.
    • Sinh học/Hóa học: Mô hình hóa phản ứng, lan truyền, tăng trưởng, …
Ví dụ:
F(x) = x2
Tại x = 2, đạo hàm bằng 4
Ý nghĩa: Nếu bạn tăng x lên một chút, thì fx tăng khoảng 4 lần so với thay đổi đó. Nói cách khác đạo hàm là cách đo độ dốc của một đường cong tại một điểm.
Ví dụ:
Vị trị s(t) của xe tại thời điểm t thì đạo hàm của nó chính là vận tốc.
Nếu bạn biết vị trí thay đổi theo thời gian như thế nào, thì đạo hàm cho bạn biết xe đang chạy nhanh hay chậm, đang tăng tốc hay giảm tốc.
Công thức:



Xử lý dữ liệu
Chuẩn hóa dữ liệu
Chuẩn hóa về [0,1]
Công thức:
Result = (x-min(x) / (max(x) - min(x))
Cho mảng arr = np.array([5, 10, 15, 20, 25]). Hãy chuẩn hóa các giá trị này về đoạn [0, 1] chỉ bằng numpy.
import numpy as np

arr = np.array([5, 10, 15, 20, 25], dtype=float)
res = (arr - arr.min()) / (arr.max() - arr.min())

print(res) # [0.   0.25 0.5  0.75 1.  ]
Hàm kích hoạt
Linear
Công thức:
z = W·X + b

Đây là cách viết phổ biến trong machine learning lý thuyết, đặc biệt trong sách Deep Learning.
Thường:

    • X: vector input kích thước (n, 1)
    • W: ma trận trọng số kích thước (m, n)
    • b: vector bias (m, 1)
z = X·W + b

Phổ biến trong framework dạng batch, như TensorFlow, PyTorch, sklearn.
Thường:

    • X: dạng hàng (row vector) hoặc batch (batch_size, n)
    • W: ma trận trọng số (n, m)
    • b: vector bias (m,)
ReLu
Hàm kích hoạt ReLU giúp phá vỡ tính tuyến tính, cho phép mạng học được các hàm số phức tạp hơn và giúp giảm thiểu hiện tượng triệt tiêu đạo hàm (vanishing gradient) so với Sigmoid hay Tanh
Công thức: 
f(x) = max(0, x)
Sigmoid
Công thức: 
f(z) = 1 / (1+e**-z) # chỉ áp dụng lên 1 giá trị của z = W*x + b
Tanh
    • Làm phi tuyến hóa (non-linearity): Giống sigmoid, giúp mô hình học các quan hệ phi tuyến.
    • Zero-centered: giá trị nằm giữa -1 và 1 → giúp gradient descent ổn định hơn so với sigmoid (giảm bias về chiều dương).
    • Giúp mạng nơ-ron sâu học hiệu quả hơn nhờ đặc tính zero-centered.
Công thức:
tanh(x) = (e**x – e**-x) / (e**x + e**-x) - nằm trong đợn -1 đến 1
Ứng dụng:
    1. Hidden layer trong mạng nơ-ron
        1. Trước đây, thường dùng trong MLP, RNN.
        2. Ví dụ: h_t = tanh(Wx_t + Uh_{t-1}) trong RNN.
    2. Chuỗi thời gian và ngôn ngữ
        1. Trong RNN / LSTM / GRU, tanh thường dùng để:
            1. Biểu diễn trạng thái ẩn (hidden state)
            2. Điều chỉnh thông tin truyền xuống các bước thời gian.
    3. Chuẩn hóa dữ liệu đầu ra
        1. Khi dữ liệu cần nằm trong khoảng [-1, 1]
    4. Phi tuyến hóa đầu ra
        1. Trong một số bài toán hồi quy giới hạn đầu ra.
Softmax
Thường được dùng ở output layer của mô hình phân loại nhiều lớp (multi-class classification). Nó biến vector đầu ra thô (logits) của mô hình thành xác suất, sao cho tổng các xác suất = 1.
Công thức:
Giả sử đầu ra của mô hình là một vector: z = [z1, z2, z3, z4, … , zn]
→ softmax(zi) = e^zi / (e^zi + … + e^zn)
Cú pháp:
import numpy as np

def softmax(x):
    exp_x = np.exp(x – np.max(x)) # Trừ max(x) để tránh tràn số khi e^x quá lớn
    return exp_x / np.sum(exp_x)

# Ví dụ:
logits = np.array([2.0, 1.0, 0.1])
probs = softmax(logits)
print("Xác suất:", probs)
print("Tổng:", np.sum(probs))

Vector hóa văn bản
One-Hot
Tạo ra một cột cho mỗi giá trị và đánh 1 tại vị trí đúng, 0 ở vị trí khác
Loss Function (Hàm mất mát) & cost function (Hàm chi phí)
Mean Squared Error (MSE)
Công thức:
MSE = 1/n . [(y_pred1 – y1)^2 + (y_pred1 – y1)^2 + … ]
Binary Cross-Entropy (Log Loss)
Dùng cho phân loại nhị phân.
Công thức:
    • Công thức cho 1 mẫu: BCE(y_true, y_pred) = −[y_true.log(y_pred) + (1-y_true).log(1−y_pred)]
    • Công thức cho batch (N mẫu): BCE = −(1/n) . [yi_true . log(yi_pred) + (1-yi_true) . log(1−yi_pred)]
    • dL/dw = (y-pred – y_true).x
    • dL/db = (y_pred - y_true)
Cú pháp:
import math

def bce(y, y_hat):
    return -(y*math.log(y_hat) + (1-y)*math.log(1-y_hat))

print(bce(1, 0.9))
print(bce(1, 0.1))

Categorical Cross-Entropy
Dùng cho phân loại nhiều nhãn
Công thức:
L = -(yi.log(y_predi) + … + )
Lỗi thường gặp & Giải pháp & Đánh giá mô hình
Accuracy
Accuracy (độ chính xác) được dùng để đánh giá độ đúng của mô hình phân loại. Nó cho biết mô hình dự đoán đúng bao nhiêu phần trăm so với toàn bộ dữ liệu.
    • Dùng cho: phân loại nhị phân, đa lớp (classification).
    • Không dùng tốt khi dữ liệu mất cân bằng (VD: 95 mẫu âm, 5 mẫu dương → đoán tất cả là âm sẽ đạt 95% accuracy nhưng vô dụng).
Công thức:
Accuracy = Số dự đoán đúng / Tổng số dự đoán
Hoặc với confusion matrix:
Accuracy=TP+TN+FP+FNTP+TN​ 
Trong đó:
    • TP: dự đoán đúng lớp dương
    • TN: dự đoán đúng lớp âm
    • FP: dự đoán sai (dự đoán dương nhưng thực tế âm)
    • FN: dự đoán sai (dự đoán âm nhưng thực tế dương)
Cú pháp:
y_true = [1, 0, 1, 1, 0]
y_pred = [1, 0, 0, 1, 1]

accuracy = sum(t == p for t, p in zip(y_true, y_pred)) / len(y_true)
print("Accuracy =", accuracy)

F1
Overfitting & Underfitting
Overfitting xảy ra khi mô hình học quá kỹ dữ liệu huấn luyện -> mất khả năng tổng quát với dữ liệu mới. Biểu hiện là accuracy trên tập huấn luyện rất cao còn trên tập test lại thấp.
Cách xử lý:
    • Thêm dữ liệu huấn luyện
    • Giảm độ phức tạp của mô hình
    • Regularization - phạt mô hình quá phức tạp
    • Early stopping cho mạng nơ ron
    • Dropout cho deep learning
    • Cross-validation (đánh giá mô hình nhiều lần với nhiều cách chia tập train/test khác nhau để tránh ăn may.
Underfitting xảy ra khi mô hình quá đơn giản hoặc thiếu dữ liệu, không thể học ra quy luật dẫn đến hiệu suất kém.

Vanishing Gradient (Gradient biến mất) & Exploding Gradient (Gradient bùng nổ)

Vanishing
Exploding

Khi huấn luyên bằng backpropagation, đạo hàm (gradient) giảm rất nhỏ qua từng lớp. Dẫn đến các lớp đầu (gần input) gần như không học được gì → Mạng hội tụ rất chậm hoặc không học được gì. Đặc biệt nghiêm trọng trong RNN do lan truyền qua nhiều bước thời gian (time steps). loss giảm chậm. 
Đạo hàm (gradient) qua từng lớp bị nhân lên quá lớn. => Dẫn đến việc cập nhật trọng số quá mạnh, mô hình không ổn định, có thể NaN.học
loss tăng vọt, nổ NaN, model không ổn định
Giải pháp
Dùng ReLu thay cho sigmoid/tanh
dùng batch Normalization
Dùng kiến trúc LSTM/GRU thay cho RNN thường
Khởi động trọng số dúng cách.
Gradient clipping: giới hạn giá trị gradient.
chọn learning rate vừa phải
khởi tạo trọng số cẩn thận
L1 & L2 regularization
Là một kỹ thuật thêm một hình phạt vào hàm mất mát để làm mô hình đơn giản hơn, tránh học quá kỹ dữ liệu huấn luyện (overfitting)
L1
L2
Giống như ép các trọng số về đúng không, chỉ giữ lại đặc trưng thật sự quan trọng.
Dùng khi muốn chọn lọc đặc trưng tự động (ví dụ mô hình có quá nhiều đặc trưng).
Giảm nhẹ tất cả trọng số, giúp mô hình ổn định hơn, tránh quá nhạy.
Dùng khi muốn giảm độ phức tạp chung của mô hình mà vẫn giữ lại toàn bộ đặc trưng.
Precision & recall
Precision
recall
Là độ chính xác của positive
precision = TP / (TP + FP) => trong số các dự đoán là positive (tích cực) có bao nhiêu cái đúng thật.
precision cao nghĩa là ít cảnh báo sai. Dùng khi chi phí của dự đoán sai là cao.
Nếu tăng Precision => dễ giảm recall (mô hình dè dặt hơn khi dự đoán positive)
Recall = TP / (TP + FN) => trong số các trường hợp thật sự là positive, mô hình bắt được bao nhiêu
Recall cao nghĩa là ít bị bỏ sót
Dùng khi cần bắt hết các trường hợp dương tính
Nếu tăng Recall => dễ gaimr Precision (mô hình mạnh tay dự đoán Positive nhưng dễ sai hơn)
Ví dụ: Hệ thống kiểm tra ung thư
Nếu precision cao tức hạn chế cảnh báo nhầm tới người khỏe mạnh còn recall cao sẽ hạn chế bỏ sót bệnh nhân thật sự. 
Nên sử dụng F1-Score (2x(PrecisionxRecall)/(Precision+Recall) => thích hợp khi cần cân bằng giữa Precision và recall
Machine Learning
Linear Regression
Đầu ra dự đoán là liên tục và có độ dốc không đổi. Nó được sử dụng để dự đoán các giá trị trong một phạm vi liên tục (doanh số, giá cả) thay vì cố gắng phân loại chúng thành các danh mục nhóm (chó, mèo).
Bài tập
Demo code thuần không dùng thư viện Linear Regression 1 đặc trưng
'''
========================================
===== LINEAR REGRESSION CODE THUẦN =====
========================================
'''
def predict(X, W, b):
    return W * X + b

def mse(X, y, W, b):
    n = len(X)
    total = 0
    for i in range(n):
        y_pred = predict(X[i], W, b)
        total += (y_pred - y[i])**2
    return total / n

def train(X, y, W, b, epochs, lr):
    n = len(X)

    for epoch in range(epochs):
        dw = 0
        db = 0

        # Gradient tính đúng
        for i in range(n):
            y_pred = predict(X[i], W, b)
            dw += (2/n) * X[i] * (y_pred - y[i])
            db += (2/n) * (y_pred - y[i])

        # Cập nhật W, b
        W = W - lr * dw
        b = b - lr * db

        if epoch % 100 == 0:
            m = mse(X, y, W, b)
            print(f"Epoch {epoch} - MSE: {m}")

    return W, b

# Dataset
X = [150, 155, 160, 165, 170, 180, 185, 190]
y = [50, 55, 60, 65, 70, 80, 85, 90]

# Khởi tạo
W = 0
b = 0

# Learning rate nên rất nhỏ
W, b = train(X, y, W, b, epochs=5000, lr=0.0000001)

print("Final W =", W)
print("Final b =", b)
print(f"Weight of human 1m76: {predict(176, W, b)}")
Xây dựng model linear 2 đặc trưng
X = [
    [150, 20],
    [155, 22],
    [160, 23],
    [165, 25],
    [170, 27],
    [180, 29],
    [185, 30],
    [190, 32]
]
y = [50, 55, 60, 65, 70, 80, 85, 90]
W = [0, 0]
b = 0

def predict(X, W, b):
    y_pred = 0
    for i in range(len(X)):
        y_pred += W[i]*X[i]
    return y_pred+b

def mse(X, y, W, b):
    n = len(X)
    m = 0
    for i in range(len(y)):
        y_pred = predict(X[i], W, b)
        m = (y_pred-y[i])**2
    return m/n

def train(X, y, W, b, epochs, lr):
    n = len(X)
    d = len(W)
    for epoch in range(epochs):
        dw = [0]*d
        db = 0 
        for i in range(n):
            y_pred = predict(X[i], W, b)
            for j in range(d):
                dw[j] += (2/n)*X[i][j]*(y_pred-y[i])
            db += (2/n)*(y_pred-y[i])
        
        for i in range(d):
            W[i] = W[i] - lr*dw[i]
        b = b - lr*db
        m = mse(X, y, W, b)
        if epoch%1000==0:
            print(f"epoch {epoch}, mse {m}, W {W}, b {b}") 
    return W, b

W, b = train(X, y, W, b, epochs=5000, lr=0.000001)

print("\n===== RESULT =====")
print("Final W:", W)
print("Final b:", b)
test = [176, 28]   # chiều cao 176cm, tuổi 28
print(f"Predict weight for height={test[0]}, age={test[1]} → {predict(test, W, b)} kg")

Train model linear với numpy
import pandas as pd
import numpy as np

# ====== Bước 1: Tạo bộ dữ liệu ======
np.random.seed(42)
thoi_gian = np.random.randint(low=5, high=30, size=30, dtype=int)
so_bai_tap = np.random.randint(low=3, high=20, size=30, dtype=int)
so_buoi_di_hoc = np.random.randint(low=2, high=8, size=30, dtype=int)

# ====== Bước 2: khởi tạo w, b đầu tiên ======
diem = 2*thoi_gian + 3*so_bai_tap + 2*so_buoi_di_hoc + np.random.normal(loc=0, scale=5, size=30)

df = pd.DataFrame({
    "thoi_gian": thoi_gian,
    "so_bai_tap": so_bai_tap,
    "so_buoi_di_hoc": so_buoi_di_hoc,
    "diem": diem
})

# ====== Bước 3: Thuật toán Linear =======
def activate_function(X, w, b):
    return np.dot(X, w) + b # x1*w1 + x2*w2 + x3*w3 + … + b

def cost_function(X, y, w, b):
    m = len(y)
    mse = 0
    for i in range(m):
        y_pred = sum([X[i][j]*w[j] for j in range(len(w))]) + b
        loss = (y[i] - y_pred)**2
        mse += loss
    return mse/m

def update_w_b(X, y, w, b, learning_rate):
    m = len(y)
    y_pred = np.dot(X, w) + b
    error = y - y_pred
    dw = -2/m * np.dot(X.T, error)
    db = -2/m * np.sum(error)

    w = w - dw*learning_rate
    b = b - db*learning_rate
    return w,b

def train(X, y, w, b, learning_rate, epoch):
    for i in range(epoch):
        w, b = update_w_b(X,y,w,b,learning_rate=learning_rate)
        if i%100 == 0:
            print("epoch: ", i, "cost: ", cost_function(X,y,w,b))
    return w, b

# ======= Bước 4: Đánh giá ======
X = df.drop('diem', axis=1).values
y = df['diem'].values
w1 = np.zeros(X.shape[1])
w, b = train(X, y, w1, 0.1, 0.0001, 1000)
print(activate_function([15, 10, 3], w, b))
Train model Linear với pytorch
import pandas as pd
import torch

data = {
    'weight': [50, 60, 70, 80, 90],
    'high': [160, 170, 172, 185, 190]
}
df = pd.DataFrame(data)

X = torch.tensor(df['weight'])
y = torch.tensor(df['high'])
W = torch.tensor(0.5, requires_grad=True)
b = torch.tensor(0.0, requires_grad=True)
lr = 0.01

for epoch in range(5):
  y_pred = W*X+b
  loss = ((y_pred-y)**2).mean()

  loss.backward()
  with torch.no_grad():
    W -= lr*W.grad
    b -= lr*b.grad

  W.grad.zero_()
  b.grad.zero_()

  print(f"Epoch {epoch}, Loss: {loss.item():.4f}, W: {W.item():.4f}, b: {b.item():.4f}")
import torch.optim as optim

optimizer = optim.SGD([W, b], lr=0.01)

for epoch in range(5):
    y_pred = W*X + b
    loss = ((y_pred - y)**2).mean()
    
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()  # cập nhật W, b tự động
Logistic Regression
Bài tập
Demo logistic với numpy
import numpy as np
import matplotlib.pyplot as plt
# dữ liệu gốc
dataSet = np.array(
    [[-10, 0],
     [-5, 0],
     [-7, 0],
     [0, 0],
     [-2, 0],
     [5, 1],
     [7, 1],
     [6, 1],
     [10, 1],
     [15, 1],
     [9, 1]
     ]
)

# phương trình đường cong được xây dựng bởi công thức logistic regression
def get_prediction(m, b, x):
return 1/(1 + np.exp(-m*x+b))

# hàm tính toán mất mát
def get_cost(y, y_hat):
    k = y.shape[0]
return (-1/k)*np.sum(y*np.log(y_hat)+(1-y)*np.log(1-y_hat))

# hàm cập nhật sao cho độ mất mát giảm dần
def get_gradient(m, b, x, y, y_hat):
    k = y.shape[0]
    dm = (1/k)*np.sum((y_hat - y)*x)
    db = (1/k)*np.sum(y_hat-y)
return dm, db

# hàm tính toán độ chính xác khi áp dụng lên bộ dữ liệu này
def get_accuracy(y, y_hat):
return ((y_hat >= 0.5).astype(int) == y).sum()/ y.shape[0]

# test mô hình
# 1 - bịa ra giá trị m, b
m = 1.0
b = 10.0
# số lần lặp lại để cập nhật lại độ mất mát
interations = 150
# learning rate - tốc độ cập nhật độ mất mát
lr = 0.03

x = dataSet[:, 0]
y = dataSet[:, 1]
# lưu cost vào một mảng
costs = []
for it in range(interations):
    y_hat = get_prediction(m, b, x)
    cost = get_cost(y, y_hat)
    # mức độ chính xác
    accuracy = get_accuracy(y, y_hat)
    print(f"iteration {it} - cost {cost}, accuracy: {accuracy}")
    dm, dn = get_gradient(m, b, x, y, y_hat)
    # cập nhật
    m -= lr*dm
    b -= lr*dn
    costs.append(cost)

iteration 0 - cost 1.2806026124548595, accuracy: 0.6363636363636364
iteration 1 - cost 1.0864043766201612, accuracy: 0.6363636363636364
iteration 2 - cost 0.9378122484032957, accuracy: 0.7272727272727273
…
…
iteration 143 - cost 0.013258107606832945, accuracy: 1.0
iteration 144 - cost 0.013141438742927412, accuracy: 1.0
iteration 145 - cost 0.013026711929090811, accuracy: 1.0
iteration 146 - cost 0.012913880600277159, accuracy: 1.0
iteration 147 - cost 0.012802899632104342, accuracy: 1.0
iteration 148 - cost 0.012693725286686972, accuracy: 1.0
iteration 149 - cost 0.012586315160851966, accuracy: 1.0
Demo Logistic với torch
Cây Quyết định
Thuật toán ID3 (Iterative Dichotomiser 3)
    • Là thuật toán xây dựng cây quyết định bằng cách chọn thuộc tính “tốt nhất” để chia dữ liệu tại mỗi bước.
    • Thuộc tính “tốt nhất” được chọn dựa trên việc giảm độ hỗn loạn (entropy) nhiều nhất → nghĩa là giúp dữ liệu trở nên “thuần” nhất có thể.
Entropy (độ hỗn loạn):
Cho biết một tập dữ liệu có lẫn lộn hay không. (Khi chia dữ liệu theo thuộc tính A thì độ hỗn loạn mới là bao nhiêu)
Công thức:
Entropy(S) = -[p1.log2(p1) + p2.log2(p2) + … ]
    • pi: phần trăm mẫu thuộc lớp i (ví dụ: [‘no’, ‘no’, ‘yes’, ‘yes’, ‘yes’] thì p_no = 2/5). Nếu tập đã thuần (100% Yes) → entropy = 0 (không hỗn loạn).
    • Nếu chia đều (50% Yes - 50% No) → entropy = 1 (hỗn loạn tối đa).
EntropyA(S) = [(|Sv1| / S) * Entropy(Sv1) + (|Sv2| / S) * Entropy(Sv2) + ...]
    • Chia dữ liệu theo thuộc tính A → thành nhiều nhóm (ví dụ “Weather” → Sunny/Rain/Windy…)
    • Tính entropy của từng nhóm.
    • Lấy trung bình theo trọng số số lượng mẫu.
Information Gain (độ tăng thông tin):
Sự giảm hỗn loạn khi chia theo thuộc tính. Thuộc tính có Information Gain cao nhất → chọn làm node.
Gain(S,A)=Entropy(S)−EntropyA(S)
    • Gain = mức giảm độ hỗn loạn khi chia bằng A.
    • A càng làm tập “thuần” hơn → Gain càng lớn → được chọn.
Bài tập
Demo cây quyết định với thuật toán id3

Deep Learning
Batch Normalization (BN)
Là một kỹ thuật giúp tăng tốc độ huấn luyện và giảm hiện tượng gradient biến mất, bằng cách chuẩn hóa (normalize) đầu ra của mỗi layer (thường là sau Conv2D hoăc Dense).
MLP (Multi-layer Perceptron)
    • Là một mạng nơ-ron nhân tạo gồm nhiều lớp tuyến tính kết hợp với các hàm kích hoạt phi tuyến.
Ứng dụng:
    • Phần loại hình ảnh, văn bản.
    • Dự đoán giá trị (hồi quy).
    • Dự đoán chuỗi thời gian.
Cấu trúc cơ bản:
    1. Input layers: Nhận dữ liệu đầu vào dạng vector.
    2. Hidden layers (1 hoặc nhiều): Mỗi lớp gồm nhiều nơ ron, mỗi neuron tính tổng có trọng số của đầu vào rồi áp dụng activation function như ReLU, sigmoid, tanh …
    3. Output layer: Trả về kết quả cuối cừng, có thể là phần loại, hồi quy, …
Cơ chế hoạt động:
    • MLP, còn được gọi là mạng truyền thẳng (Feedforward Network), được cấu tạo từ các lớp (layer): Lớp đầu vào, một hoặc nhiều lớp ẩn, và lớp đầu ra.
    • 1. Phép nhân Ma trận (Matrix Multiplication):
        ◦ Đây là cơ chế cốt lõi để tính toán đầu ra của một nơ-ron trong lớp tiếp theo.
        ◦ Đối với mỗi nơ-ron trong lớp ẩn, đầu vào của nó là tổng có trọng số của đầu ra từ tất cả các nơ-ron trong lớp trước.
        ◦ Công thức tổng quát cho tính toán tuyến tính (linear combination) trong một lớp là: Z=XW+B
            ▪ X: Ma trận đầu vào từ lớp trước (hoặc lớp đầu vào).
            ▪ W: Ma trận trọng số (Weights) của lớp hiện tại. Đây là các tham số mà mô hình học được.
            ▪ B: Vector độ lệch (Bias) của lớp hiện tại.
            ▪ Z: Đầu ra tuyến tính.
    • 2. Hàm Kích Hoạt Phi Tuyến tính (Non-linear Activation Function)
        ◦ Sau khi tính toán tuyến tính (Z), kết quả này sẽ được truyền qua một hàm kích hoạt (ví dụ: Sigmoid, ReLU, Tanh).
        ◦ Công thức: A=f(Z)
            ▪ A: Đầu ra đã được kích hoạt (activation), đây chính là đầu vào cho lớp tiếp theo.
            ▪ f: Hàm kích hoạt phi tuyến tính.
Tầm quan trọng: Cơ chế này là quan trọng nhất vì nếu không có hàm kích hoạt phi tuyến tính, dù MLP có bao nhiêu lớp đi chăng nữa, nó vẫn chỉ có thể mô hình hóa các mối quan hệ tuyến tính (giống như hồi quy tuyến tính). Khả năng học các mối quan hệ phức tạp và phi tuyến tính của dữ liệu (ví dụ: phân loại hình ảnh, dịch máy) đến từ việc sử dụng các hàm kích hoạt này.

Bài tập
Demo cách hoạt động của MLP
Đề bài: Cho input là [1,2,3,4,5] và mạng nơ ron 2 lớp 3x2. Demo cách hoạt động của mạng nơ ron này
    1. Khởi tạo tham số ban đầu:
       w11 = [0.1, 0.2, 0.3, 0.4, 0.5], b11 = 0.01
       w12 = [0.11, 0.22, 0.33, 0.44, 0.55], b12 = 0.01
       w13 = [0.15, 0.25, 0.35, 0.45, 0.55], b13 = 0.01
       w21 = [0.1, 0.2, 0.3], b21 = 0.01
       w22 = [0.05, 0.15, 0.2], b21 = 0.01
    2. Tíng giá trị z của mỗi nơ ron:
       z11 = 1x0.1 + 2x0.2 + 3x0.3 + 4x0.4 + 5.0.5 + 0.01 = 5.51
       z12 = 6
       z13 = 6.4
    3. Áp dụng hàm kích hoạt ReLU cho layer 1:
       h11 = 5.51
       h12 = 6
       h13 = 6.4
    4. Tính giá trị z cho mỗi nơ ron ở layer 2:
       z21 = 0.1x5.51 + 0.2x6 + 0.3x6.4 = 3.67
       z22 = 2.58
    5. Áp dụng softmax cho layer 2: softmax = [0.748, 0.252]
    6. Tính độ mất mát (loss) bằng Categorical Cross-Entropy với nhãn thật là [1,0]:
       L = -(1.log(0.748) + 0.log(252)) = 0.126
    7. Backpropagation:
       dL/dz2k = d2k = pk – yk
       …
    8. Cập nhật lại trọng số và bias
       w := w -alpha*&w
       b := b – alpha*&b
Xây dựng mạng neural 1 lớp 2 nơ ron
NLP
Text preprocessing (Xử lý văn bản)
Text Normalization / Text cleaning
Chuẩn hóa văn bản trước khi tách token.
Tokenization Methods
Các kỹ thuật tạo token.
Token
Là một đơn vị nhỏ mà mô hình NLP sử dụng để xử lý văn bản. Nó không nhất thiết phải là một từ:
    • Một từ: ví dụ "bật", "nhạc"
    • Một từ gốc: "chơi" từ "chơi nhạc"
    • Một tiếng (âm tiết): trong tiếng Việt rất phổ biến
    • Thậm chí là một nửa từ (vì mô hình học theo kiểu cắt nhỏ)
Cú pháp:
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("vinai/phobert-base")
sentence = "bật nhạc lofi chill"
tokens = tokenizer.tokenize(sentence)

print(tokens) # ['bật', 'nhạc', 'lo', '##fi', 'chill']
Word-level Tokenization
    • Cắt câu theo dấu cách hoặc dấu câu. Không xử lý được từ mới (OOV), không phù hợp với ngôn ngữ biến hình (như tiếng Việt, tiếng Đức…).
    • Dùng trong mô hình NLP cổ điển như Bag-of-Words, TF-IDF, Word2Vec, LSTM cũ,...
Bag of Word (BoW)
    • Cho phân loại văn bản đơn giản → Không cần học sâu
    • Phù hợp khi cần nhanh, độ chính xác tương đối tốt, câu ngắn, cấu trúc cố định, từ vững rõ ràng.
    • Có thể sử dụng sklearn (CountVectorizer)
N-gram
    • Phổ biến với TF-IDF và BoW → Hiểu concept, không cần học sâu
    • Ý tưởng đơn giản: chia chuỗi ký tự/word thành các nhóm liên tiếp độ dài N.
        ◦ Unigram = từng token / từ riêng lẻ.
        ◦ Bigram = từng cặp từ liên tiếp.
        ◦ Trigram = bộ 3 từ liên tiếp.
    • nắm bắt ngữ cảnh cục bộ (ví dụ “New York” là bigram, có ý nghĩa khác so với hai từ riêng). Dùng trong: language modelling, feature cho classification, spelling correction, autocomplete.
    • Ví dụ dễ hiểu (word-level):
        ◦ Câu: “tôi yêu học AI”
        ◦ Unigrams: [“tôi”, “yêu”, “học”, “AI”]
        ◦ Bigrams: [“tôi yêu”, “yêu học”, “học AI”]
    • Ưu: đơn giản, hiệu quả cho nhiều task.
    • Nhược: số lượng feature bùng nổ khi N tăng; cần smoothing cho language model.
TF-IDF
    • Vẫn rất mạnh với các bài toán: spam, phân loại tin nhắn, search engine. → Quan trọng mức trung bình (chỉ cần hiểu công thức)
    • Ý tưởng đơn giản: tính trọng số cho từ dựa trên mức độ “quan trọng” của nó trong một document so với toàn bộ corpus.
        ◦ TF (term frequency): tần suất từ xuất hiện trong một tài liệu.
        ◦ IDF (inverse document frequency): giảm trọng số của từ xuất hiện ở nhiều tài liệu (ví dụ “và”, “the”).
    • vector hóa văn bản cho classification, search (retrieval), scoring (document ranking).
    • Ví dụ ngắn: Nếu “AI” xuất hiện nhiều trong một doc (TF cao) nhưng ít xuất hiện trong corpus (IDF cao) → TF-IDF cho “AI” lớn → từ quan trọng cho doc đó.
    • Ưu: đơn giản, hiệu quả cho văn bản ngắn và retrieval.
    • Nhược: bỏ qua thứ tự từ/ngữ cảnh; tính lạc hậu với embedding contextual.
Subword Tokenization
Đây là phương pháp đứng sau các mô hình hiện đại như. PhoBERT, BARTpho, XLM-R, mBERT, GPT, LLaMA, Qwen, v.v. VÀ sống khỏe trong mọi hệ thống NLP từ 2020 đến 2025. Nếu bạn học sâu 1 thứ → hãy học cái này.
BPE (Byte Pair Encoding)
    • Là một kỹ thuật tokenization hiện đại và phổ biến nhất dùng trong GPT-2, GPT-3, RoBERTa, XLM-R, PhoBERT. Rộng rãi nhất trong các mô hình open-source → Học sâu
    • bằng cách ghép các cặp ký tự/subword phổ biến nhất. 
    • BPE phải có </w>? Vì BPE hoạt động bằng cách merge các cặp ký tự/token, và nếu không có end marker, BPE sẽ merge xuyên qua ranh giới giữa các từ → làm hỏng cấu trúc từ.
Bài tập
BPE thực chất là tổng hợp của các bài toán nhỏ hơn. Thông qua các bài tập nhỏ này có thể ghép lại và code được BPE
Tách chuỗi "hello" thành ["h", "e", "l", "l", "o"]
def split(text: str):
    return [t for t in text]
Nối các phần tử của mảng ["he", "l", "lo"] thành "he l lo"
def split(li: list):
    return ' '.join(li)

print(split(["he", "l", "lo"])) # he l lo
Tách chữ thành ký tự và đếm tần suất mỗi ký tự
def counts(lines: list):
    # 1. Tách ký tự và gộp thành 1 list
    chars = []
    for line in lines:
        for ch in line:
            if ch != " ":       # bỏ khoảng trắng
                chars.append(ch)
    
    # 2. Đếm tần suất
    freq = {}
    for ch in chars:
        freq[ch] = freq.get(ch, 0) + 1

    return freq

print(counts(["hello world", "hello"]))
Tạo danh sách tất cả các cặp ký tự liền nhau
def bigrams_from_string(s: str):
    return [(s[i], s[i+1]) for i in range(len(s)-1)]

print(bigrams_from_string("hello")) # [('h','e'), ('e','l'), ('l','l'), ('l','o')]
Tìm bigram xuất hiện nhiều nhất
def most_bigram_frequency(big: list):
    # big: list of tuple
    freq = {}
    for b in big:
        freq[b] = freq.get(b, 0) + 1

    best_count = -1
    best_bigram = None
    for k, v in freq.items():
        if v > best_count:
            best_count = v
            best_bigram = k

    return freq, (best_bigram, best_count)

input_data = [("h","e"), ("e","l"), ("l","l"), ("l","o")]
print(most_bigram_frequency(input_data))
# Expected: ({('h','e'):1, ('e','l'):1, ('l','l'):1, ('l','o'):1}, (('h','e'),1))
# Note: all have count 1 so first-seen is returned as "best"
from collections import Counter

def most_bigram_frequency(big: list):
    cnt = Counter(big)
    if not cnt:
        return {}, (None, 0)
    most_common_bigram, freq = cnt.most_common(1)[0]
    return dict(cnt), (most_common_bigram, freq)

input_data = [("h","e"), ("e","l"), ("l","l"), ("l","o")]
print(most_bigram_frequency(input_data))
from collections import Counter

def most_bigram_frequency(big: list):
    cnt = Counter(big)
    if not cnt:
        return {}, (None, 0)
    most_common_bigram, freq = cnt.most_common(1)[0]
    return dict(cnt), (most_common_bigram, freq)

input_data = [("h","e"), ("e","l"), ("l","l"), ("l","o")]
print(most_bigram_frequency(input_data))
Replace một bigram trong danh sách token
def replace_pair(tokens_list, pair, new_token):
    out = []
    for tokens in tokens_list:
        merged = []
        i = 0
        while i < len(tokens):
            if i < len(tokens)-1 and (tokens[i], tokens[i+1]) == pair:
                merged.append(new_token)
                i += 2
            else:
                merged.append(tokens[i])
                i += 1
        out.append(merged)
    return out

WordPiece
    • Phổ biến nhất trong BERT, RoBERTa, ALBERT, … → Biết cách dùng, không cần học sâu (ít mô hình mới dùng)
    • Là thuật toán tách từ thành các mảnh nhỏ (subword). Mục tiêu chính:
        ◦ Giảm số lượng từ trong vocab, vì nhiều từ hiếm → khó học.
        ◦ Xử lý từ mới (OOV - out of vocabulary): nếu mô hình chưa từng thấy từ đó, nó vẫn có thể hiểu nhờ các mảnh subword.
    • Giống BPE nhưng tối ưu bằng xác suất có điều kiện: BERT, mBERT, DistilBERT
Ví dụ:
Với câu "playing plays played"
    1. Bắt đầu: [p][l][a][y][i][n][g]
    2. Ghép thường xuyên: "pl", "play"
    3. Tiếp tục học "##ing", "##ed", "##s"
→ Cuối cùng vocab có thể gồm: ["[PAD]", "[UNK]", "play", "##ing", "##ed", "##s"]
Cú pháp:
from transformers import BertTokenizer

# Dùng tokenizer của BERT (WordPiece)
tokenizer = BertTokenizer.from_pretrained("bert-base-uncased")

sentence = "Playing football is amazing"
tokens = tokenizer.tokenize(sentence)
ids = tokenizer.convert_tokens_to_ids(tokens)

print("Tokens:", tokens)
print("IDs:", ids)
Tokens: ['playing', 'football', 'is', 'amazing']
IDs: [2652, 2374, 2003, 6429]
# Nếu bạn nhập từ mới lạ như "playfulness", BERT chưa từng thấy nguyên từ đó, nhưng WordPiece vẫn xử lý được

tokens = tokenizer.tokenize("playfulness")
print(tokens)
['play', '##ful', '##ness']
Unigram Language Model (SentencePiece)
    • Dùng trong T5, mT5, UL2, PaLM, Flan series. Mạnh cho đa ngôn ngữ. → Học khá sâu
    • Chọn subword tối ưu bằng mô hình ngôn ngữ xác suất.
Byte-level BPE
    • Tokenize thẳng trên bytes → không phụ thuộc unicode. Dùng trong GPT-2, GPT-3, GPT-4, LlaMA-3. → Hiểu khái niệm là đủ (rất giống BPE)
    • Biến thể của BPE ở cấp byte, xử lý tốt đa ngôn ngữ, emoji, ký tự lạ. GPT-2, GPT-3, GPT-4, LLaMA-2/3
Transformer embeddings
Phù hợp khi cần mô hình hiểu ngữ cảnh phức tạp, dữ liệu đa dạng, ngôn ngữ tự nhiên đầy đủ, nhiều dữ liệu huấn luyện (ít nhất vài nghìn câu)
CRF
Character-level Tokenization
    • Tách từng ký tự, không bao giờ OOV.
    • Nhược điểm: chuỗi rất dài, học chậm, mất ngữ nghĩa cao cấp.
    • Ứng dụng: các mô hình nghiên cứu ngôn ngữ đặc biệt (ví dụ xử lý lỗi chính tả, OCR, mã hóa DNA,…). Dùng trong Char-CNN, Char-RNN, hoặc một số mô hình hybrid (kết hợp subword + char).
Post-Tokenization Processing
Xử lý token sau khi tách
Stopwords removal
    • Ý tưởng: danh sách các từ “không mang nhiều ý nghĩa” như “và”, “là”, “the”, “a” — thường loại bỏ trước khi xử lý để giảm noise và kích thước feature.
    • Tiền xử lý — giảm kích thước bộ từ và tăng chất lượng feature cho TF/Count.
    • Lưu ý: với một số tác vụ (ví dụ sentiment, questions), stopwords có thể mang thông tin (ví dụ “not” cực kỳ quan trọng) → cẩn thận khi loại.
Stemming
    • Ý tưởng: Cắt đuôi từ để đưa về dạng gốc thô bằng cách dùng rule cứng (heuristics). Không quan tâm ngữ pháp. Không đảm bảo trả về từ có nghĩa.
    • Cách làm: cắt suffix kiểu “ing”, “ed”, “ly”, “s”, …
    • Dùng để làm gì: giảm số lượng dạng của từ, đơn giản hoá văn bản để dùng cho TF-IDF, bag-of-words, search,…
Lemmatization
    • Ý tưởng: đưa từ về dạng nguyên mẫu có nghĩa (lemma) dựa trên từ điển + phân tích ngữ pháp. Dùng mô hình ngôn ngữ / từ điển. Trả về từ hợp lệ của ngôn ngữ. Hiểu ngữ cảnh của từ trong câu.
    • xử lý NLP có yêu cầu ngữ nghĩa tốt hơn information extraction, question answering, machine translation

sentence segmentation
Embedding & Vector Representation
CBOW
Skip-gram
Glove
Transformer embedding
Luồng hoạt động:
raw text → token → token_id → padding → attention mask → embedding lookup → positional encoding → final transformer embedding

Positional Encoding
    • Với câu “tôi ăn cơm” Token embedding của Transformer không biết 3 từ này đang ở vị trí 1–2–3 hay 3–2–1, vì attention không có tính tuần tự như RNN. Ta phải cộng thêm 1 vectơ đại diện cho “vị trí số mấy trong câu” → Đó là positional encoding.
    • Ví dụ:
        1. Token IDs: 
           [1, 2, 3, 4]
        2. Lookup embedding → mỗi token thành vector 3 chiều
           token embeddings = [
               [1, 2, 3],      # token 1
               [4, 5, 6],      # token 2
               [7, 8, 9],      # token 3
               [10,11,12]      # token 4
           ]
           → Đây là Embedding → học được ý nghĩa của từ.
        3. Positional Encoding (PE):
           PE = [
               [0,    0,    0   ],   # vị trí 0
               [1,    1,    1   ],   # vị trí 1
               [2,    2,    2   ],   # vị trí 2
               [3,    3,    3   ],   # vị trí 3
           ]
        4. Cộng embedding + positional encoding theo từng vị trí
           [
               [1,  2,  3 ],
               [5,  6,  7 ],
               [9, 10, 11 ],
               [13,14, 15 ]
           ]

Công thức:
Với vị trí pos và chiều vector I
    • PE(pos, 2i) = sin(pos/10000**(2i/d))
    • PE(pos, 2i+1) = cos(pos/10000**(2i/d)
Tức là token ở vị trí 0,1,2,3,… sẽ có vector chứa sin/cos có tần số khác nhau. Mỗi chiều dùng tần số khác nhau → mô hình phân biệt được vị trí.
Công thức nâng cao chunt Hugging Face:
    • a**b = e**(b.ln(a)) → 10000**(2i/d) = e**(ln(10000) . (2i/d))
Ví dụ:
Giả sử embedding size = 4 (d = 4)
Vị trí token = 2
Ta tính:
Với i = 0:
    • chiều 0 (even): PE(2,0)=sin⁡(2 / (10000**(0/4))=sin⁡(2)=0.9093
    • chiều 1 (odd): PE(2,1)=cos⁡(2 / (10000**(0/4))=cos⁡(2)=−0.4161
Với i = 1:
    • chiều 2 (even): PE(2,2)=sin⁡(2/100001/4)≈sin⁡(2/10)=sin⁡(0.2)=0.1987
    • chiều 3 (odd): PE(2,3)=cos⁡(2/100001/4)=cos⁡(0.2)=0.9801
Positional embedding cho vị trí 2: [ 0.9093,  -0.4161,  0.1987,  0.9801 ]
Cú pháp:
import torch
import math

def positional_encoding(seq_len, d_model):
    PE = torch.zeros(seq_len, d_model)
    
    for pos in range(seq_len):
        for i in range(d_model):
            angle = pos / (10000 ** (2 * (i // 2) / d_model))
            if i % 2 == 0:
                PE[pos, i] = math.sin(angle)
            else:
                PE[pos, i] = math.cos(angle)

    return PE


pe = positional_encoding(seq_len=5, d_model=8)
print(pe)
tensor([
 [0.0000, 1.0000, 0.0000, 1.0000, ...],  # pos=0
 [0.8415, 0.5403, 0.0100, 1.0000, ...],  # pos=1
 [0.9093,-0.4161, 0.0200, 0.9998, ...],  # pos=2
 ...
])
def positional_encoding_fast(seq_len, d_model):
    position = torch.arange(seq_len).unsqueeze(1)
    div_term = torch.exp(torch.arange(0, d_model, 2) * (-math.log(10000.0) / d_model))

    PE = torch.zeros(seq_len, d_model)
    PE[:, 0::2] = torch.sin(position * div_term)
    PE[:, 1::2] = torch.cos(position * div_term)
    return PE

PhoBERT
RNN (Recurrent Neural Network)
    • Là một loại mạng neural dùng để xử lý dữ liệu tuần tự (sequential data). RNN hoạt động dựa trên ý tưởng: thông tin ở bước t−1 sẽ được kết hợp với đầu vào ở bước t để tạo ra trạng thái mới.
    • Thay vì xử lý từng input một cách độc lập như MLP (Multilayer Perceptron), RNN giữ lại trạng thái (state) từ bước trước đó và sử dụng nó để xử lý input hiện tại. Điều này rất phù hợp với: Chuỗi văn bản, Dữ liệu thời gian (time series), Chuỗi tín hiệu âm thanh, video…
    • Có một khái niệm quan trong là hidden state (trí nhớ tạm thời của RNN tại thời điểm đó).
    • Ý tưởng: Mỗi bước thơi gian lấy input + trạng thái cũ → tạo trạng thái mới
    • Vấn đề: 
        ◦ RNN quên rất nhanh.
        ◦ Không nhớ được thông tin xa.
        ◦ Bị vanishing gradient khi chuỗi dài.
        ◦ Bạn đọc câu: "Tôi ăn cơm lúc 7h sáng, và đến chiều thì tôi đói." RNN có thể không nhớ phần trước (7h sáng) vì quá xa → mất ngữ cảnh → RNN phù hợp với chuỗi ngắn, hoặc tác vụ đơn giản.
BPTT (Backpropagation Through Time)
    • Đây là kỹ thuật tính gradient cho RNN. Vì RNN có trạng thái ẩn h_t phụ thuộc vào tất cả các h_(t-1), h_(t-2), …, nên backprop bình thường không đủ, ta phải "trải graph ra theo thời gian" và tính gradient qua từng step.
    • Về cơ bản: BPTT là backpropagation chuẩn, nhưng áp dụng lên graph được unfold theo time steps.
    • Công thức: dL/dW = sum((dL/dh_t) . (dh_t/dW))
Cú pháp:
# Forward RNN qua seq_len steps
h = torch.zeros(batch, hidden_dim)
for t in range(seq_len):
    h = torch.tanh(X[:, t, :] @ Wxh + h @ Whh + bh)

# Loss dựa trên h cuối
loss = cross_entropy(h @ Why + by, y)

# BPTT
loss.backward()  # PyTorch tự lan truyền qua tất cả h_t
Bài tập
Demo RNN bằng torch
import torchimport torch.nn as nn
import torch.optim as optim

# Dữ liệu: mapping từ chữ cái sang số
chars = sorted(list(set("hello")))
char2idx = {ch: idx for idx, ch in enumerate(chars)}
idx2char = {idx: ch for ch, idx in char2idx.items()}

# Dữ liệu huấn luyện
seq = "hell"
target = "ello"

# Biến đổi thành tensor
input_seq = torch.tensor([char2idx[ch] for ch in seq])  # [h, e, l, l]
target_seq = torch.tensor([char2idx[ch] for ch in target])  # [e, l, l, o]

# Đưa về định dạng batch_size x seq_len
input_seq = input_seq.unsqueeze(0)
target_seq = target_seq.unsqueeze(0)

# Tham số mô hình
vocab_size = len(chars)
embedding_dim = 10
hidden_dim = 20

# Mô hình RNN
class RNNModel(nn.Module):
    def __init__(self):
        super(RNNModel, self).__init__()
        self.embedding = nn.Embedding(vocab_size, embedding_dim)
        self.rnn = nn.RNN(embedding_dim, hidden_dim, batch_first=True)
        self.fc = nn.Linear(hidden_dim, vocab_size)

    def forward(self, x):
        x = self.embedding(x)  # [batch, seq, embed_dim]
        out, _ = self.rnn(x)   # [batch, seq, hidden_dim]
        out = self.fc(out)     # [batch, seq, vocab_size]
        return out

model = RNNModel()
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.01)

# Huấn luyện
for epoch in range(100):
    optimizer.zero_grad()
    output = model(input_seq)
    loss = criterion(output.view(-1, vocab_size), target_seq.view(-1))
    loss.backward()
    optimizer.step()
    if epoch % 10 == 0:
        print(f"Epoch {epoch}, Loss: {loss.item():.4f}")

# Dự đoán tiếp theo
with torch.no_grad():
    out = model(input_seq)
    predicted_idx = torch.argmax(out, dim=2).squeeze().tolist()
    predicted_chars = ''.join([idx2char[idx] for idx in predicted_idx])
    print("Dự đoán:", predicted_chars)

import torchimport torch.nn as nn
import torch.optim as optim

# Dữ liệu: mapping từ chữ cái sang số
chars = sorted(list(set("hello")))
char2idx = {ch: idx for idx, ch in enumerate(chars)}
idx2char = {idx: ch for ch, idx in char2idx.items()}

# Dữ liệu huấn luyện
seq = "hell"
target = "ello"

# Biến đổi thành tensor
input_seq = torch.tensor([char2idx[ch] for ch in seq])  # [h, e, l, l]
target_seq = torch.tensor([char2idx[ch] for ch in target])  # [e, l, l, o]

# Đưa về định dạng batch_size x seq_len
input_seq = input_seq.unsqueeze(0)
target_seq = target_seq.unsqueeze(0)

# Tham số mô hình
vocab_size = len(chars)
embedding_dim = 10
hidden_dim = 20

# Mô hình RNN
class RNNModel(nn.Module):
    def __init__(self):
        super(RNNModel, self).__init__()
        self.embedding = nn.Embedding(vocab_size, embedding_dim)
        self.rnn = nn.RNN(embedding_dim, hidden_dim, batch_first=True)
        self.fc = nn.Linear(hidden_dim, vocab_size)

    def forward(self, x):
        x = self.embedding(x)  # [batch, seq, embed_dim]
        out, _ = self.rnn(x)   # [batch, seq, hidden_dim]
        out = self.fc(out)     # [batch, seq, vocab_size]
        return out

model = RNNModel()
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.01)

# Huấn luyện
for epoch in range(100):
    optimizer.zero_grad()
    output = model(input_seq)
    loss = criterion(output.view(-1, vocab_size), target_seq.view(-1))
    loss.backward()
    optimizer.step()
    if epoch % 10 == 0:
        print(f"Epoch {epoch}, Loss: {loss.item():.4f}")

# Dự đoán tiếp theo
with torch.no_grad():
    out = model(input_seq)
    predicted_idx = torch.argmax(out, dim=2).squeeze().tolist()
    predicted_chars = ''.join([idx2char[idx] for idx in predicted_idx])
    print("Dự đoán:", predicted_chars)

LSTM (Long Short-Term Memory)
    • Để giải quyết việc mất trí nhớ của RNN, LSTM tách biệt hoàn toàn hai khái niệm: Hidden State (trạng thái ẩn) và Cell State (trạng thái ô - đóng vai trò như một đường băng chuyền thông tin xuyên suốt). Thêm cấu trúc “cổng” (gate) và có cell state giúp duy trì thông tin dài hạn.
    • Cơ chế 3 Cổng (Gates): Hãy tưởng tượng Cell State là một băng tải chạy dọc từ đầu đến cuối chuỗi. Các cổng sẽ quyết định cái gì được đặt lên hoặc nhấc ra khỏi băng tải đó:
        ◦ Forget Gate (Cổng quên): "Chúng ta nên bỏ bớt cái gì cũ không?"
            ▪ Nó nhận đầu vào xt​ và ht−1​, đi qua hàm Sigmoid (cho ra giá trị từ 0 đến 1).
            ▪ Nếu là 0: Xóa bỏ hoàn toàn thông tin cũ. Nếu là 1: Giữ lại toàn bộ.
        ◦ Input Gate (Cổng vào): "Có thông tin mới nào đáng giá để lưu lại không?"
            ▪ Gồm 2 phần: Một hàm Sigmoid quyết định cập nhật cái gì và một hàm tanh tạo ra một vector giá trị mới tiềm năng để đưa vào Cell State.
        ◦ Output Gate (Cổng ra): "Từ những gì đang có, chúng ta nên xuất bản cái gì ra ngoài?"
            ▪ Nó quyết định giá trị nào trong Cell State sẽ được dùng để tạo ra Hidden State (ht​) cho bước tiếp theo. LSTM có 3 cổng: Forget - Input – Output
    • Ưu điểm: Nhớ được thông tin xa hơn, Giảm vanishing gradient, Ổn định hơn khi xử lý văn bản dài
GRU (Gated Recurrent Unit)
    • GRU (Gated Recurrent Unit) là một phiên bản "tối giản" của LSTM. Nó ra đời sau (vào năm 2014) với mục tiêu làm cho mạng nơ-ron hồi tiếp chạy nhanh hơn và tốn ít bộ nhớ hơn nhưng vẫn giữ được khả năng "nhớ lâu" của LSTM.
    • 3 sự thay đổi lớn so với LSTM:
        1. Hợp nhất hai trạng thái thành một: Trong khi LSTM tách biệt Cell State (Ct​ - trí nhớ dài hạn) và Hidden State (ht​ - trí nhớ ngắn hạn), thì GRU gộp chúng lại làm một. GRU chỉ dùng duy nhất Hidden State (ht​) để truyền tải thông tin xuyên suốt qua các bước thời gian. Điều này giúp cấu trúc của nó gọn nhẹ hơn hẳn.
        2. Cơ chế 2 Cổng (Gates) thay vì 3: GRU không dùng "Cổng quên" riêng biệt và "Cổng vào" riêng biệt. Thay vào đó, nó dùng: Update Gate (Cổng cập nhật): Đây là sự kết hợp giữa Cổng quên và Cổng vào của LSTM. Nó quyết định xem bao nhiêu phần trăm thông tin cũ từ quá khứ cần giữ lại, và bao nhiêu phần trăm thông tin mới sẽ được nạp vào. Ví dụ: Nếu giá trị cổng là 0.7, nó có thể hiểu là giữ 70% cũ và nạp thêm 30% mới.
    • Reset Gate (Cổng đặt lại): Cổng này quyết định xem nên "quên" bao nhiêu thông tin từ trạng thái ẩn trước đó để tính toán thông tin mới (candidate state). Nó giúp mô hình loại bỏ những thông tin không còn liên quan đến ngữ cảnh hiện tại.
Transformer
Positional encoding
Giúp mô hình biết vị trí từ trong câu, vì cơ chế Attention không tự biết thứ tự
Công thức:
    • PEpos,2i = sin(pos/10000^(2i/dmodel))
    • PEpos,2i+1 = cos(pos/10000(2i/dmodel))
        ◦ pos: vị trí từ trong câu
        ◦ i: chỉ số chiều embedding
        ◦ d_model: chiều embedding (thường 512, 768…)
Bài tập
Demo về positional encoding
import torch
import torch.nn.functional as F
import matplotlib.pyplot as plt
import math

# Câu demo: 5 từ
words = ["Tôi", "yêu", "học", "máy", "."]
seq_len = len(words)
d_model = 8  # embedding nhỏ để minh họa

# Token embedding giả (random)
torch.manual_seed(0)
token_embeddings = torch.rand(seq_len, d_model)

# Hàm Positional Encoding
def positional_encoding(max_len, d_model):
    pe = torch.zeros(max_len, d_model)
    for pos in range(max_len):
        for i in range(0, d_model, 2):
            pe[pos, i] = math.sin(pos / (10000 ** ((2*i)/d_model)))
            if i+1 < d_model:
                pe[pos, i+1] = math.cos(pos / (10000 ** ((2*i)/d_model)))
    return pe

pe = positional_encoding(seq_len, d_model)

# Cộng token embedding + PE
x = token_embeddings + pe
print("Embedding + Positional Encoding:\n", x)
Self-Attention
    • Attention (đặc biệt là Self-Attention) chính là "linh hồn" giúp Transformer hiểu được ngữ cảnh mà không cần xử lý tuần tự từng từ như RNN hay LSTM.
    • Nếu RNN/LSTM giống như việc bạn đọc một cuốn sách từ trái sang phải và cố gắng nhớ những gì đã qua, thì Attention giống như việc bạn nhìn vào một từ và ngay lập tức "liếc" sang tất cả các từ khác trong câu để hiểu nghĩa của nó.
1. Tại sao Attention lại "thắng" RNN/LSTM?

Trong RNN/LSTM, thông tin phải đi qua một "nút thắt cổ chai" (vector trạng thái ẩn). Nếu câu quá dài, thông tin từ đầu câu sẽ bị mờ nhạt dần khi đến cuối câu.

Attention giải quyết bằng cách: Cho phép mỗi từ (token) kết nối trực tiếp với tất cả các từ khác, bất kể khoảng cách.

    Ví dụ: Trong câu "Con mèo nằm trên thảm vì nó mệt".

        Cơ chế Attention sẽ giúp từ "nó" kết nối mạnh nhất với từ "con mèo".

        Mô hình hiểu ngay ngữ cảnh: "nó" ở đây là "con mèo" chứ không phải "cái thảm".

2. "Bộ ba nguyên tử": Query, Key, Value (Q, K, V)

Để tính toán xem "nên chú ý vào đâu", Attention sử dụng một hệ thống giống như việc tìm kiếm thông tin trong thư viện:

    Query (Q - Truy vấn): "Tôi là từ hiện tại, tôi đang tìm kiếm mối liên quan gì?"

    Key (K - Khóa): "Tôi là các từ khác trong câu, tôi có đặc điểm này, liệu có khớp với bạn không?"

    Value (V - Giá trị): "Nếu tôi và bạn liên quan đến nhau, đây là thông tin nội dung mà tôi sẽ đóng góp cho bạn."

Quy trình tính toán:

    Lấy Query nhân với Key của tất cả các từ khác để ra một con số (điểm số tương quan).

    Dùng hàm Softmax để biến các con số đó thành tỷ lệ phần trăm (ví dụ: chú ý vào chính nó 70%, chú ý vào từ 'mèo' 20%, các từ khác 10%).

    Nhân tỷ lệ này với các Value tương ứng để tạo ra vector đại diện mới mang đầy đủ ngữ cảnh.
Điểm yếu của Attention (để trả lời sâu hơn)

Dù mạnh mẽ, Attention có một nhược điểm chí mạng: Độ phức tạp tính toán.

    Vì mỗi từ phải "nhìn" tất cả các từ khác, nên nếu câu có n từ, số phép tính sẽ là n2 (bình phương).

    Đây là lý do tại sao các mô hình như ChatGPT có giới hạn về "Context Window" (độ dài văn bản đầu vào) – vì nếu input quá dài, lượng RAM và năng lượng tính toán sẽ tăng vọt theo cấp số nhân.
Multi-head Attention
    • Multi-Head Attention = nhiều self-attention “head” chạy song song
    • Mỗi head học một khía cạnh khác nhau của ngữ cảnh
    • Output cuối cùng = concat tất cả head → linear layer
Công thức:
Attention(Q, K, V) = softmax(Q.k^T/sqrt(dk)).V
Bài tập
Demo Multi-head Attention
import torch
import torch.nn.functional as F

# Câu demo: 4 từ
words = ["Tôi", "yêu", "AI", "."]
seq_len = len(words)
d_model = 8  # embedding nhỏ để minh họa
num_heads = 2  # 2 head

# Token embedding giả
torch.manual_seed(0)
x = torch.rand(seq_len, d_model)

# Chia embedding cho mỗi head
d_k = d_model // num_heads

# Tạo Q,K,V weights cho mỗi head
W_Q = torch.rand(num_heads, d_model, d_k)
W_K = torch.rand(num_heads, d_model, d_k)
W_V = torch.rand(num_heads, d_model, d_k)

heads = []
for h in range(num_heads):
    Q = x @ W_Q[h]  # (seq_len, d_k)
    K = x @ W_K[h]
    V = x @ W_V[h]
    
    # Attention score
    scores = Q @ K.T / (d_k ** 0.5)
    attn = F.softmax(scores, dim=-1)
    
    # Weighted sum
    head_out = attn @ V
    heads.append(head_out)

# Concat các head
multi_head_out = torch.cat(heads, dim=-1)
print("Multi-Head Attention output shape:", multi_head_out.shape)
print("Multi-Head Attention output:\n", multi_head_out)

BERT (Bidirectional Encoder Representations from Transformers)
    • Là một mô hình ngôn ngữ do Google phát triển (2018), dùng để hiểu ngữ cảnh của câu theo cả hai chiều (trái → phải và phải → trái) và được xây dựng chỉ dùng phần encoder của transformer.
    • BERT không tạo văn bản mới (như GPT), mà hiểu và biểu diễn ngữ nghĩa câu chữ. Nó được dùng như "bộ não ngôn ngữ" trong các bài toán hiểu ngôn ngữ tự nhiên (NLU).
Nhiệm cụ của BERT:
    • BERT chỉ là một bộ biểu diễn ngữ nghĩa. BERT mã hóa câu hoặc từ thành vector chứa ngữ cảnh 2 chiều. 
    • Ví dụ với hai câu: "Tôi ăn no rồi", "Tôi đã no bụng" → BERT sẽ biến mỗi câu thành một vector 768 chiều (nếu dùng bert-base), và vì nghĩa tương tự → 2 vector gần nhau trong không gian embedding.
Pipeline hoạt động của BERT:
Inputs → input Embedding + Positional Encoding → Multi-head Attention → Add & Norm → Feed Forward → Add & Norm → Linear → Softmax → Output
GPT (Generative Pre-trained Transformer)
    • Là mô hình của OpenAI dùng decoder của Transformer để: Sinh văn bản (generate), chứ không phải hiểu như BERT.
    • GPT được huấn luyện để:
        ◦ Dự đoán token tiếp theo trong chuỗi
        ◦ Học cách viết mượt, logic, tự nhiên
        ◦ Hoàn thành câu, sinh câu trả lời, dịch, viết code,…
        ◦ Bạn có thể xem GPT như bộ não viết/generate, trong khi BERT là bộ não phân tích/understand.
Dùng để làm gì:
    • Sinh văn bản: viết bài, viết code, tóm tắt
    • Chatbot hội thoại: ChatGPT chính là GPT + RLHF
    • Hoàn thành câu / dự đoán token tiếp theo: Cho nửa câu, GPT viết tiếp
    • Dịch, rewrite, paraphrase
    • Sinh câu trả lời hỏi đáp (free-form)
Pipline của GPT:
    • Input: "Tôi đang đói nên tôi muốn"
    • GPT làm:
        1. Tokenize câu
        2. Áp vào Transformer Decoder
        3. Dự đoán token tiếp theo: "ăn"
        4. Ghép vào chuỗi → tiếp tục dự đoán token tiếp theo nữa
        5. Dừng khi gặp token kết thúc
Bài tập
Demo Fine-Tune Chatbot Hỏi-Đáp bằng transformer
from transformers import AutoTokenizer, AutoModelForCausalLM, Trainer, TrainingArguments
from datasets import load_dataset

model_name = "Qwen/Qwen2.5-7B-Instruct"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name)

# Load dữ liệu
dataset = load_dataset("csv", data_files={"train": "data.csv"})

# Tokenize
def preprocess(example):
    text = f"### User: {example['input']}\n### Assistant: {example['response']}"
    tokens = tokenizer(text, truncation=True, padding="max_length", max_length=512)
    tokens["labels"] = tokens["input_ids"].copy()  # labels = input_ids cho LM
    return tokens

tokenized_dataset = dataset["train"].map(preprocess, batched=False)

# Training
training_args = TrainingArguments(
    output_dir="./chatbot_model",
    per_device_train_batch_size=2,
    num_train_epochs=1,
    save_steps=100,
    logging_steps=10,
    fp16=True  # nếu GPU hỗ trợ
)

trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=tokenized_dataset
)

trainer.train()

Seq2Seq (Sequence-to-Sequence)
    • Là mô hình nhận một chuỗi đầu vào và tạo ra một chuỗi khác đầu ra.
    • Kiểu như:
        ◦ dịch câu → từ tiếng Việt sang tiếng Anh
        ◦ tóm tắt văn bản
        ◦ chatbot trả lời tin nhắn
        ◦ biến dãy số → dãy số khác

    • Cấu trúc chuẩn gồm:
        ◦ Encoder: đọc chuỗi đầu vào, nén thông tin thành vector ngữ cảnh.
        ◦ Decoder: dùng vector đó để tạo chuỗi đầu ra từng bước một.
Bài tập
Biến chuỗi ký tự viết thường bằng chuỗi ký tự viết hoa
import torch
import torch.nn as nn

# ----- 1. Simple Seq2Seq model -----
class Encoder(nn.Module):
    def __init__(self, vocab, hidden):
        super().__init__()
        self.embed = nn.Embedding(vocab, hidden)
        self.rnn = nn.GRU(hidden, hidden)

    def forward(self, x):
        emb = self.embed(x)
        output, h = self.rnn(emb)
        return h  # context


class Decoder(nn.Module):
    def __init__(self, vocab, hidden):
        super().__init__()
        self.embed = nn.Embedding(vocab, hidden)
        self.rnn = nn.GRU(hidden, hidden)
        self.fc = nn.Linear(hidden, vocab)

    def forward(self, x, h):
        emb = self.embed(x)
        output, h = self.rnn(emb, h)
        return self.fc(output), h


class Seq2Seq(nn.Module):
    def __init__(self, enc, dec):
        super().__init__()
        self.enc = enc
        self.dec = dec

    def forward(self, src, trg):
        h = self.enc(src)
        outputs = []
        dec_in = trg[0].unsqueeze(0)   # start token
        for _ in range(1, trg.size(0)):
            out, h = self.dec(dec_in, h)
            outputs.append(out)
            dec_in = out.argmax(-1)   # greedy decode
        return torch.stack(outputs)

# ----- 2. Mini example -----
vocab = 30
hidden = 32
enc = Encoder(vocab, hidden)
dec = Decoder(vocab, hidden)
model = Seq2Seq(enc, dec)

src = torch.tensor([[1, 5, 8]])   # "a,b,c"
trg = torch.tensor([[2, 6, 9]])   # expected uppercase

out = model(src, trg)
print(out.shape)   # (seq_len-1, batch, vocab)

Computer Vision
Kênh  màu
    • Mặc định Opencv sử dụng kênh màu BGR.
    • Vì OpenCV ban đầu đưuọc viết bằng C/C++ và theo chuẩn xử lý ảnh của Windows Bitmap (BMP) - vốn lưu pixel theo thứ tự BGR. Để tăng hiệu suất và tránh chuyển đổi không cần thiết, OpenCV giữ nguyên thứ tự này.
    • Khi đọc ảnh từ file, OpenCV đọc pixel theo thứ tự BGR để tránh tốn tài nguyên chuyển đổi qua lại nếu bạn xử lý nhiều ảnh ở cấp hệ thống.
Segmentation mask là gì?
    • Là một ảnh đen trắng (hoặc đa kênh) dùng để biểu diện phân vùng (vật thể hoặc khu vực) trong ảnh gốc
        ◦ Mỗi pixel trong mask cho biết vật thể nào (hoặc lớp nào) nó thuộc về.
        ◦ Có 2 loại phổ biến:
            ▪ binary mask: pixel=1 nếu thuộc vật thể, 0 nếu là nền.
            ▪ multi-class mask: pixel =0,1,2,… tương ứng với các lớp khác nhau (mèo, chó, người, …).
    • Không phụ thuộc vào màu sắc, mà phụ thuộc vào nhãn mà bạn gán khi huấn luyện mô hình.
Multi-channel image
Là ảnh có nhiều kênh màu.
Depth - Độ sâu
    • Là số lớp (layers) trong mô hình.
    • Tăng depth → mô hình học được tính chất phức tạp hơn.
Width - Độ rộng
    • Là số lương filters (kernels) mỗi lớp convolution.
    • Tăng width → mỗi lớp trích xuất ddwuocj nhiều đặc trưng hơn.
    • Ví dụ: Có nhiều người cùng quan sát vào một ảnh → mỗi người chú ý vào đặc điểm khác nhau.
Resolution - Độ phân giải ảnh
    • Là kích thước ảnh đầu vào (224x224 → 380x380).
    • Tăng resolution → mô hình nhìn thấy chi tiết nhỏ hơn.
    • Ví dụ: Cùng một bức tranh, nếu ảnh lớn hơn thì nhìn rõ mắt, mũi, lông mi, ...
Kernel
    • Phần lớn các bộ lọc đều dựa trên khái niệm convolution (tích chập) – tức là áp một ma trận (kernel) lên từng vùng nhỏ của ảnh để tính toán giá trị mới cho pixel trung tâm. Cách áp dụng kernel này có một quy tắc chuẩn:
    • Duyệt từng pixel trong ảnh gốc.
    • Với mỗi pixel, lấy vùng lân cận (theo kích thước kernel), nhân chéo với kernel.
    • Tính tổng và gán giá trị kết quả vào pixel tương ứng trong ảnh mới.
Ví dụ:
Với bộ lọc làm mờ trung bình (mean blur), kernel là ma trận các số bằng nhau, cộng lại rồi chia trung bình.
 Sự khác nhau của các bộ lọc:
Tùy loại bộ lọc mà kernel hoặc cách áp dụng sẽ khác nhau:
Bộ lọc
Cách hoạt động đặc trưng
Làm mờ (blur)
Tính trung bình vùng lân cận – làm giảm chi tiết, nhiễu.
Gaussian Blur
Dùng kernel theo phân phối Gauss – làm mờ mịn, tự nhiên hơn.
Median Blur
Lấy giá trị trung vị trong vùng lân cận – khử nhiễu muối tiêu.
Sharpen (làm sắc nét)
Dùng kernel làm nổi bật cạnh, tăng tương phản cục bộ.
Sobel, Laplacian
Dùng để phát hiện biên cạnh – áp kernel đạo hàm.
Bộ lọc tùy chỉnh
Người dùng định nghĩa kernel riêng và áp dụng tương tự.
Bài tập
Cho một ma trận ảnh 5×5 và một kernel 3×3, hãy tính kết quả tích chập (convolution)
import numpy as np

img = np.array([
    [1,2,3,4,5], 
    [6,7,8,9,10],
    [11,12,13,14,15],
    [16,17,18,19,20],
    [21,22,23,24,25]
])
kernel = np.array([
    [2,4,6],
    [1,2,3],
    [3,4,5]
])

h, w = img.shape
kh, kw = kernel.shape
out_h = h - kh + 1
out_w = w - kw + 1

# ✅ Tạo mảng kết quả có kích thước sẵn
out = np.zeros((out_h, out_w))

for i in range(out_h):
    for j in range(out_w):
        out[i, j] = np.sum(img[i:i+kh, j:j+kw] * kernel)

print(out)
[[178. 202. 226.]
 [298. 322. 346.]
 [418. 442. 466.]]
Chuẩn hóa
Bài tập
Chuẩn hóa ảnh về [0,1]
x_train = x_train.astype('float32') / 255.0
x_test  = x_test.astype('float32') / 255.0
Preprocessing (Các kỹ thuật tiền xử lý ảnh)
CLAHE (Contrast Limited Adaptive Histogram Equalization)
    • Mục đích chính của kỹ thuật này là tăng cường độ tương phản (contrast) cục bộ của hình ảnh.
    • Nó giúp làm nổi bật các chi tiết trong các vùng ảnh quá tối hoặc quá sáng mà các phương pháp tăng cường độ tương phản toàn cục (như Histogram Equalization truyền thống) không xử lý tốt, thậm chí còn gây ra nhiễu hoặc làm mất chi tiết.
    • Bạn nên sử dụng kỹ thuật CLAHE khi bạn có những bức ảnh gặp vấn đề về độ tương phản, đặc biệt là khi sự chênh lệch độ sáng (dynamic range) trong ảnh lớn hoặc có những vùng bị tối/sáng cục bộ.
    • Các trường hợp cụ thể thường áp dụng CLAHE bao gồm:
        ◦ Xử lý Ảnh Y học (Medical Imaging): Ảnh chụp X-quang, MRI, CT, ảnh soi đáy mắt (như trong chẩn đoán bệnh lý về mắt) thường có độ tương phản thấp hoặc có các vùng chi tiết cần làm nổi bật. CLAHE giúp tăng khả năng hiển thị các cấu trúc sinh học.
        ◦ Ảnh trong Điều kiện Ánh sáng Kém: Ảnh chụp trong điều kiện thiếu sáng hoặc có ánh sáng nền mạnh (backlit), nơi chi tiết bị "chìm" trong bóng tối hoặc bị "cháy" sáng.
        ◦ Hệ thống Thị giác Máy (Machine Vision) và Xử lý Ảnh: Khi cần tiền xử lý ảnh (preprocessing) để chuẩn hóa hoặc tăng cường chất lượng ảnh đầu vào trước khi đưa vào các thuật toán nhận dạng, phân loại, hoặc học sâu (Deep Learning/CNN). Việc này giúp thuật toán trích xuất đặc trưng (feature extraction) chính xác hơn.
        ◦ Ảnh Thiên văn hoặc Viễn thám: Ảnh vệ tinh hoặc ảnh chụp từ kính thiên văn thường cần CLAHE để làm rõ các cấu trúc và đặc điểm bề mặt.
    • Ưu điểm của CLAHE so với HE truyền thống
        ◦ CLAHE là một cải tiến của phương pháp Cân bằng Biểu đồ màu (Histogram Equalization - HE) truyền thống:
        ◦ Adaptive (Thích nghi): Thay vì áp dụng sự cân bằng độ tương phản cho toàn bộ ảnh, CLAHE chia ảnh thành nhiều ô (tiles/regions) nhỏ và áp dụng HE cho từng ô riêng biệt. Điều này giúp tăng cường độ tương phản cục bộ mà không làm ảnh hưởng đến các vùng khác.
        ◦ Contrast Limited (Giới hạn Độ tương phản): CLAHE có một tham số giới hạn (clip limit) để ngăn chặn việc độ tương phản bị tăng quá mức ở các vùng nhiễu (noise) hoặc các vùng có độ tương phản rất thấp, giúp tránh tình trạng nhiễu bị khuếch đại (over-amplification).
Model (Mô hình)
CNN (Convolutional Neural network)
    • Được thiết kế để xử lý dữ liệu có cấu trúc dạng lưới, ví dụ như hình ảnh.
    • Convolutional: Thay vì kết nối mọi input với mọi nơ ron như MLP, CNN sử dụng một bộ lọc nhỏ (filter hoặc kernel) trượt trên ảnh đầu vào để lấy ra những đặc trưng nhỏ như cạnh, góc, hay các mẫu đơn giản. Bộ lọc này sẽ quét khắp ảnh. Phát hiện các đặc điểm quan trọng tại nhiều vị trí. Mỗi kernel học một đặc trưng khác nhau
    • Pooling: Giúp giảm kích thước dữ liệu sau khi tích chấp, làm cho mạng nhẹ hơn, giảm tính toán, đồng thời giữ lại đặc trưng quan trọng. Ví dụ, max pooling chọn giá trị lớn nhất trong một vùng nhỏ.
    • Fully connected: Sau các lớp convolutional và pooling, dữ liệu đặc trưng được dàn phẳng và dựa vào các lớp MLP để phân loại hay dự đoán.
Conv2D:
Lớp Conv sâu hơn thường học đã trưng trừu tượng hơn (edge → shape → object)
RetinaNet
    • Là một mô hình deep learning dùng để phát hiện và phân loại nhiều vật thể trong ảnh (object detection), ví dụ tìm xe, người, mèo, chó trong cùng một ảnh.
    • retinaNet giả quyết một vấn đề cuecj lớn trong object detection gọi là imbalance (mất cân bằng) giữa các vùng có vật thể và vùng không có vật thể.
    • RetinaNet sử dụng một kỹ thuật tên là Focal Loss => nhờ đó mô hình tập trung học tốt hơn ở những vùng khó, không bị lười học ở các vùng dễ.
        ◦ Nếu mô hình đoán đúng và tự tin → loss rất nhỏ.
        ◦ Nếu mô hình đoán sai → loss rất lớn.
        ◦ Nhưng nếu mô hình đoán đúng mà không tự tin → loss vẫn tương đối cao → khuyến khích cải thiện.
    • Cấu trúc:
        ◦ Backbone (ResNet50, ResNet101): Trích xuất đặc trưng.
        ◦ Feature Pyramid Network (FPN): Giúp phát hiện vật thể ở nhiều kích cỡ.
        ◦ Two Subnets:
            ▪ Classification subnet: phân loại mỗi anchor box.
            ▪ Regression subnet: dự đoán bounding box cho từng object.
    • Dùng RetinaNet khi cần độ chính xác tốt hơn YOLO, làm việc với ảnh có nhiều vật thể nhỏ hoặc nhiều lớp khác nhau, muốn thử nghiệm focal loss cho bài toán mất cân bằng.
Inception
    • Là một kiến trúc mạng nơ-ron tích chập (CNN), nó kết hợp nhiều kernel khác nhau chạy song song và sau đó gộp kết quả lại, nhằm giúp mô hình vừa học được chi tiết nhỏ, vừa nhìn được tổng thể.
    • Cách hoạt động:
        ◦ Tạo nhiều nhánh song song.
        ◦ Mooic nhánh xử lý cùng một input - tức sao chép ảnh gốc cho nhiều nhánh.
        ◦ Mỗi nhánh áp dụng một loại xử lý khác nhau, ví dụ:
            ▪ Nhánh 1: Convolution 1x1
            ▪ Nhánh 2: Convolution 1x1 → 3x3
            ▪ Nhánh 3: Convolution 1x1 → 5x5
            ▪ Nhánh 4: MaxPooling 3x3 → Convolution 1x1
        ◦ Gộp kết quả từ tất cả các nhanh theo chiều channel.
MobileNet - Mạng nhẹ cho di động
    • Mô hình VGG hay ResNet rất mạnh nhwung quá nặng, không chạy nổi trên điện thoại hoặc thiết bị trên IoT.
    • Mô hình sử dụng kỹ thuật Depthwise Separable Convolution, thay vì dùng Convolution thường.
        ◦ Depthwise Separable tách ra làm 2 bước → Nhệ hơn 8-9 lần so với Conv chuẩn mà vẫn giữ được độ chính xác.
            ▪ Depthwise Convolution - Xử lý từng kênh riêng biệt (nhẹ hơn rất nhiều).
            ▪ Pointwise Convolution - Dùng Conv 1x1 để kết hợp các kênh lại.
EfficientNet - Mạng cân bằng cả tốc độ và độ chính xác
    • Dùng MobileNet thì nhẹ nhwung độ chính xác hơi kém so với ResNet. Dùng ResNet thì chính xác nhưng chậm.
    • EfficientNet dùng kỹ thuật Compound Scaling để cân bằng giữa độ sâu, độ rộng, và độ phân giải đầu vào.
    • Cấu trúc:
        ◦ Dùng khối MBConv (Mobile Inverted Bottleneck) giống MobileNetV2.
        ◦ Thêm SE Block (Squeeze-and-Excitation) để học kênh nào quan trọng.
        ◦ Dùng Swish hoạc SiLU activation thay cho ReLU để tăng độ mượt.
SSD - Single Shot Detector
    • Phát hiện vật thể trong 1 lần quét ảnh (sigle shot).
    • Nhanh, nhẹ, dùng tốt cho real-time (ảnh từ wwebcam, robot, …)
Faster R-CNN
    • Phát hiện vật thể chính xác cao nhưng chậm hơn YOLO.
    • Gồm 2 bước: Xác định vùng → nhận diện vật thể.
    • Dùng khi cần độ chính xác cao, ít quan trọng tốc độ.
U-Net
    • Phân đoạn ảnh y tế (VD: Tách khối u khỏi ảnh chụp CT).
    • Inout là ảnh, output là mặt nạ (mask) có cùng kích thước.
    • Cực kỳ hiệu quả với ảnh nhỏ, ít dữ liệu.
Mask R-CNN
    • Phát hiện + phân đoạn vật thể (VD: viền rõ từng người, từng con mèo, …).
    • Nâng cấp từ Fastẻ R-CNN + thêm mặt nạ phân đoạn.
    • Output: Bounding box + Class + Mask.
DeepLab (V3, V3+)
    • Phân đoạn ảnh toàn cục (sematic segmentation).
    • Biết từng pixel là cái gì (VD: pixel này là người, kia là đường, …).
    • Rất mạnh trong phân đoạn cảnh quan, bản đồ, ảnh vệ tinh.
OpenPose
    • Dự đoán vị trí khớp cơ thể người (pose estimation).
    • Trích ra được: Đầu, vai, tay, chân, … từ ảnh/video.
MediaPipe
    • Thư viện của Google, hỗ trợ real-time:
    • Nhận diện tay, pose, tracking, …
    • Rất nhẹ và chạy được trên điện thoại
HRNet - High Resolution Network
    • Dự đoán khớp người, phân đoạn ảnh với độ chi tiết cao.
    • Giữ ảnh độ phân giải lớn suốt mạng → chính xác hơn OpenPose.
VGG-Face
Facenet
OpenFace
DeepFace
ArcFace
Dlib
Sface
Kỹ thuật xử lý ảnh
ROI (Region Of Interest)
    • Trong cả bức ảnh / frame, mình chỉ quan tâm một vùng nào đó, còn lại thì kệ.
    • Ví dụ đời thường:
        ◦ Camera giao thông → chỉ quan tâm phần đường, không quan tâm bầu trời
        ◦ Camera lớp học → chỉ quan tâm khu vực bảng
        ◦ Camera an ninh → chỉ quan tâm cửa ra vào
    • ROI không phải AI, nó là xử lý ảnh thuần.

Detection
Cách tạo và sử dụng file data.yaml
    • File data.yaml là file cấu hình bắt buộc khi bạn muốn huấn luyện mô hình YOLOv8 trên bộ dữ liệu tùy chỉnh của mình.
    • File này có nhiệm vụ thông báo cho mô hình YOLO biết:
        ◦ Vị trí của dữ liệu: Đường dẫn đến các tập tin ảnh và nhãn (labels) cho huấn luyện, đánh giá và kiểm thử.
        ◦ Số lượng lớp (classes): Tổng số loại đối tượng mà mô hình cần học cách nhận diện.
        ◦ Tên của các lớp: Tên dễ đọc của từng loại đối tượng (ví dụ: person, car, dog).
    • File data.yaml là một file văn bản thuần túy và phải tuân theo cú pháp YAML.
Ví dụ:
Giả sử bạn có một thư mục chứa dữ liệu có tên là my_custom_dataset. Cấu trúc file mẫu sẽ trông như sau:
# data.yaml cho bộ dữ liệu tùy chỉnh

# Đường dẫn gốc (tùy chọn, nếu không có, các đường dẫn dưới đây là tuyệt đối hoặc tương đối với thư mục hiện tại)
path: /path/to/my_custom_dataset 

# Đường dẫn tương đối đến thư mục ảnh huấn luyện (Training images)
train: images/train 

# Đường dẫn tương đối đến thư mục ảnh đánh giá (Validation images)
val: images/val 

# Đường dẫn tương đối đến thư mục ảnh kiểm thử (Test images) - Tùy chọn
# test: images/test 

# Số lượng lớp (classes)
nc: 2 

# Tên của các lớp, phải theo thứ tự từ 0 đến nc-1
names: ['cat', 'dog']

Cú pháp:
from ultralytics import YOLO

# 1. Tải mô hình cơ sở (base model)
model = YOLO('yolov8n.pt')  # Sử dụng mô hình nano (n)

# 2. Định nghĩa đường dẫn đến file data.yaml của bạn
data_config_file = 'my_custom_dataset/data.yaml' 

# 3. Bắt đầu quá trình huấn luyện
# Tham số 'data' chỉ định vị trí của file cấu hình dữ liệu
# Tham số 'epochs' chỉ định số lần lặp lại huấn luyện
# Tham số 'imgsz' chỉ định kích thước ảnh đầu vào
print(f"Bắt đầu huấn luyện mô hình với cấu hình dữ liệu: {data_config_file}")

results = model.train(
    data=data_config_file, 
    epochs=100, 
    imgsz=640
)

print("Quá trình huấn luyện đã hoàn thành.")

# --- Hoặc sử dụng nó để đánh giá mô hình đã huấn luyện ---
# metrics = model.val(data=data_config_file)
YOLO ((You Only Look Once))
    • YOLO là một mô hình mạng nơ-ron tích chập (CNN) được thiết kế để thực hiện tác vụ phát hiện vật thể (Object Detection) trong thời gian thực. Cái tên "You Only Look Once" nói lên điểm cốt lõi: nó xử lý toàn bộ hình ảnh chỉ trong một lần duy nhất.
    • A. Ba phần chính của kiến trúc. Mô hình YOLO có cấu trúc tương tự như một dòng chảy dữ liệu qua 3 phần chính, hoạt động tuần tự:
        1. Backbone (Phần Trích xuất Đặc trưng)
            ▪ Mục đích: Hút các đặc trưng cơ bản từ ảnh (các cạnh, góc, hình dạng).
            ▪ Vị trí trong code: Các lớp từ (0) đến (9):
            ▪ Conv (Convolution): Lớp tích chập cơ bản, dùng để trích xuất đặc trưng.
            ▪ Conv2d(3, 16, kernel_size=(3, 3), stride=(2, 2)): Khởi đầu với ảnh 3 kênh màu (RGB), tạo ra 16 kênh đặc trưng, giảm kích thước ảnh (stride=2).
            ▪ C2f (Cross-Stage Partial Network): Là một khối kiến trúc quan trọng trong YOLO hiện đại (như YOLOv8). Nó giúp tăng hiệu suất bằng cách tách luồng đặc trưng ra hai nhánh và hợp nhất lại. Nó giúp mô hình học sâu hơn mà vẫn giữ được tốc độ.
            ▪ SPPF (Spatial Pyramid Pooling Fast): Lớp (9). Nó tổng hợp thông tin từ nhiều kích thước khác nhau của cùng một đặc trưng. Điều này giúp mô hình nhận diện vật thể bất kể kích thước của chúng (ví dụ: một chiếc xe ô tô to hay nhỏ trong ảnh).
       2. Neck (Phần Hợp nhất Đặc trưng)
            ▪ Mục đích: Kết hợp các đặc trưng đã học được từ các cấp độ sâu khác nhau của Backbone.
            ▪ Các lớp nông (gần đầu) có đặc trưng về chi tiết, vị trí chính xác.
            ▪ Các lớp sâu (gần cuối) có đặc trưng về ngữ cảnh, phân loại vật thể.
            ▪ Vị trí trong code: Các lớp từ (10) đến (21):
            ▪ Upsample (10, 13): Phóng to bản đồ đặc trưng từ lớp sâu lên.
            ▪ Concat (11, 14, 17, 20): Nối (ghép) bản đồ đặc trưng đã được phóng to với bản đồ đặc trưng tương ứng từ Backbone.
            ▪ Mô hình này sử dụng kiến trúc kiểu FPN/PAN: giúp các lớp dự đoán (Head) có được thông tin chi tiết lẫn thông tin ngữ cảnh.
        3. Head (Phần Dự đoán)
            ▪ Mục đích: Lấy các đặc trưng đã được hợp nhất từ Neck và chuyển chúng thành kết quả dự đoán cuối cùng.
            ▪ Vị trí trong code: Lớp (22) Detect(...).
            ▪ Đầu ra của Head:
            ▪ Hộp bao (Bounding Box): Toạ độ (x,y,w,h) của vật thể.
            ▪ Độ tin cậy vật thể (Objectness Score): Xác suất có vật thể trong hộp đó.
            ▪ Xác suất lớp (Class Probability): Xác suất vật thể đó thuộc về mỗi loại lớp (người, chó, xe hơi...).
            ▪ DFL (Distribution Focal Loss): Được sử dụng trong YOLOv8 để cải thiện độ chính xác của hộp bao bằng cách học cách phân phối khoảng cách tới các cạnh của hộp.

Segmentation
Không những detect nó sẽ tô màu lên vùng vật thể được detection.
Bài tập
Demo segmentation yolov8-seg
from ultralytics import YOLO
model = YOLO('model_detect/yolov8n-seg.pt')
res = model("img/predict_1.jpg")
for r in res:
    r.show()
Pose estimation
    • Là kỹ thuật dự đoán tọa độ các keypoints (điểm chính) trên đối tượng, ví dụ: Người: đầu, vai, khuỷu tay, cổ tay, hông, đầu gối, mắt cá chân… Vật thể: góc hộp, chân bàn, cánh tay robot…
    • Pose estimation thường chia thành:
        ◦ 2D Pose Estimation: Keypoints trong không gian 2D (x, y)
        ◦ 3D Pose Estimation: Keypoints có thêm độ sâu (x, y, z)
    • Nhận diện hành động người, phân tích thể thao, ứng dụng thể dục, làm phim, game, vfx, hệ thống giám sát & an ninh, robot, tương tác ảo, y học

OCR (Optical Character Recognition)
    • Là công nghệ nhận dạng ký tự quang học. Nó là một quá trình chuyển đổi hình ảnh chứa văn bản (chẳng hạn như tài liệu đã quét, ảnh chụp hoặc tệp PDF) thành văn bản mà máy tính có thể đọc, tìm kiếm và chỉnh sửa được.
    • Quy trình OCR thường bao gồm các bước sau:
    1. Thu nhận hình ảnh: Tài liệu được quét hoặc chụp ảnh. Phần mềm OCR sẽ phân tích hình ảnh này, xác định các vùng sáng (nền) và vùng tối (văn bản).
    2. Tiền xử lý: Hình ảnh được làm sạch và tối ưu hóa để cải thiện độ chính xác nhận dạng. Các bước này có thể bao gồm: 
        a) Chỉnh sửa độ nghiêng: Điều chỉnh lại hình ảnh nếu nó bị lệch khi quét.
        b) Loại bỏ nhiễu: Xóa các điểm hoặc vệt không mong muốn trên hình ảnh.
        c) Làm rõ nét: Tăng độ tương phản và làm sắc nét các ký tự.
        d) Phân đoạn: Chia hình ảnh thành các dòng, từ và ký tự riêng lẻ.
    3. Nhận dạng ký tự: Phần mềm OCR sử dụng các thuật toán và mô hình để so sánh từng ký tự đã phân đoạn với các mẫu ký tự đã được lưu trữ. Có hai phương pháp chính: 
        a) So khớp mẫu (Pattern Matching): So sánh trực tiếp hình dạng của ký tự với các mẫu có sẵn.
        b) Nhận dạng đặc trưng (Feature Recognition): Phân tích các đặc điểm độc đáo của ký tự (ví dụ: đường cong, góc) và so sánh chúng với các đặc trưng đã biết.
    4. Hậu xử lý: Văn bản đã nhận dạng có thể được kiểm tra lỗi chính tả, ngữ pháp và định dạng lại cho phù hợp.
    • Các ứng dụng phổ biến của OCR:
        ◦ Chuyển đổi tài liệu giấy sang định dạng kỹ thuật số: Giúp dễ dàng lưu trữ, tìm kiếm và chỉnh sửa.
        ◦ Trích xuất dữ liệu từ hóa đơn, biên lai, và các tài liệu khác: Tự động hóa việc nhập liệu.
        ◦ Nhận dạng biển số xe: Sử dụng trong hệ thống giao thông thông minh.
        ◦ Hỗ trợ người khiếm thị: Chuyển văn bản thành giọng nói.
        ◦ Dịch thuật: Nhận dạng văn bản trong ảnh để dịch sang ngôn ngữ khác.
        ◦ Tìm kiếm văn bản trong ảnh hoặc tệp PDF không tìm kiếm được.
Tóm lại, OCR là một công nghệ quan trọng giúp chuyển đổi thông tin từ dạng hình ảnh sang dạng văn bản có thể xử lý được bằng máy tính, mang lại nhiều lợi ích trong việc quản lý dữ liệu và tự động hóa quy trình.
Kỹ thuật tối ưu
GIL (Global Interpreter Lock)
    • GIL (Global Interpreter Lock) là một cơ chế khóa trong CPython (trình thông dịch Python phổ biến nhất). Tại mọi thời điểm, chỉ có 1 thread được phép thực thi Python bytecode, dù máy có nhiều CPU core.
    • Ví dụ:
        ◦ Thread: 1 người cầm chìa khóa (GIL), nhiều người xếp hàng
        ◦ Process: mỗi người có chìa khóa riêng chạy độc lập
Xử lý đa luồng & đa tiến trình
Bài tập
Demo threading với đọc và hiển thị camera
import cv2
import threading
import time

cap = cv2.VideoCapture(0)
frame = None
running = True

def read_camera():
    global frame
    while running:
        time.sleep(0.1)          # giả lập camera chậm
        ret, f = cap.read()
        if ret:
            frame = f

t = threading.Thread(target=read_camera, daemon=True)
t.start()

while True:
    if frame is not None:
        cv2.imshow("Demo", frame)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        running = False
        break

cap.release()
cv2.destroyAllWindows()

Học tăng cường
25.1 Giới thiệu
Học tăng cường là không ai hướng dẫn học bằng cách thử nghiệm, nhận phản hồi và điều chỉnh.