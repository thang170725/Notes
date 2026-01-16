Torch
Để xây dựng và huấn luyện mô hình học sâu (deep learning).
pip install torch
Tensor()
Để tạo tensor trong pytorch, giống với mảng số.
Cú pháp:
X = torch.tensor(X, requires_grad=True, dtype=torch.float32)
    • requires_grad=True: Cho phép PyTorch theo dõi tensor để tính gradient (W = torch.randn(3, 3, requires_grad=True))
import torch

li = torch.tensor([1,2,3,4])
print(li, li[0], type(li)) # tensor([1, 2, 3, 4]) tensor(1) <class 'torch.Tensor'>
[]
    embedding_matrix = torch.randn(10, 5)  # vocab_size=100, d_model=16
    batch = [[1,2],[3,4]]
    print(embedding_matrix)
    out = embedding_matrix[torch.tensor(batch)]
    print(out)
    print(out.shape)
tensor([[-0.0291, -1.4964,  0.5289, -0.7408, -0.9910],
        [ 1.4053,  0.3906,  0.6657,  0.5563,  0.3010],
        [ 0.2426, -0.1891, -1.8524,  0.7597, -0.8307],
        [-0.5278,  0.8487, -0.5334, -2.0883, -0.9867],
        [-1.0494,  0.9180, -2.0481,  0.2418,  0.0732],
        [-0.0869,  0.5328,  0.4544, -1.5288, -0.9604],
        [ 0.8380, -2.1501,  0.6361,  0.0210, -0.5974],
        [-0.1633, -0.1661,  1.0151, -0.9994, -1.8404],
        [ 0.0644, -1.3434, -1.8502, -0.8763,  0.0859],
        [-0.9508, -1.2242,  0.9311,  0.1119, -2.1378]])
tensor([[[ 1.4053,  0.3906,  0.6657,  0.5563,  0.3010],
         [ 0.2426, -0.1891, -1.8524,  0.7597, -0.8307]],

        [[-0.5278,  0.8487, -0.5334, -2.0883, -0.9867],
         [-1.0494,  0.9180, -2.0481,  0.2418,  0.0732]]])
torch.Size([2, 2, 5])
import torch

a = torch.arange(0, 40).reshape(10, 4)
print(a)
print(a[:, 0::2])
tensor([[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11],
        [12, 13, 14, 15],
        [16, 17, 18, 19],
        [20, 21, 22, 23],
        [24, 25, 26, 27],
        [28, 29, 30, 31],
        [32, 33, 34, 35],
        [36, 37, 38, 39]])
tensor([[ 0,  2],
        [ 4,  6],
        [ 8, 10],
        [12, 14],
        [16, 18],
        [20, 22],
        [24, 26],
        [28, 30],
        [32, 34],
        [36, 38]])

.item()
Để hiển thị giá trị của tensor. Tensor phải có duy nhất một giá trị.
Cú pháp:
a = torch.tensor([1.0, 2.0, 3.0])
W = torch.tensor([0.1, 0.2, 0.3], requires_grad=True)
b = torch.tensor(1.0, requires_grad=True)
y = W*a+b
z = torch.sum(y)
print(z.item()) # 4.4
empty()
ones()
.shape
import torch

device = torch.device("cuda" if torch.cuda.is_available() else 'cpu')
a = torch.tensor([1,2,3,4]).to(device)
print(a.shape)
torch.Size([4])
.size()
h_t = torch.zeros(1, 3)
Whh = torch.tensor([0.1, 0.2, 0.3], requires_grad=True)
print(h_t.size(), Whh.size()) # torch.Size([1, 3]) torch.Size([3])

add()
add_()
.mean()
Cú pháp:
a = torch.tensor([1.0, 2.0, 3.0, 4.0, 5.0], dtype=)
print(a.mean()) # tensor(3.)
.view()
Thay đổi hình dạng của tensor. Thay đổi shape mà không sao chép dữ liệu.
Cú pháp:
device = torch.device("cuda" if torch.cuda.is_available() else 'cpu')
a = torch.tensor([[1,2], [3,4]]).to(device)
print(a.shape)
b = a.view(4,1)
print(b.shape, b)
torch.Size([2, 2]) torch.Size([4, 1]) tensor([[1], [2], [3], [4]], device='cuda:0')
device = torch.device("cuda" if torch.cuda.is_available() else 'cpu')
a = torch.tensor([[1,2], [3,4]]).to(device)
print(a.shape)
b = a.view(-1,1)
c = a.view(1,-1)
print(b.shape, c.shape)
torch.Size([2, 2]) torch.Size([4, 1]) torch.Size([1, 4])

.backward() & .grad
    • Lan truyền ngược (backpropagation) - tính đạo hàm của loss theo từng trọng số mô hình.
    • Cập nhật trọng số mô hình theo gradient đã tính từ backward() và thuật toán tói ưu (Adam)
Cú pháp:
import torch
x = torch.tensor(2.0, requires_grad=True)
y = x**2
y.backward()  # Tính đạo hàm y theo x
print(x)
print(x.grad) # gradient được lưu trong x.grad
tensor(2., requires_grad=True)
tensor(4.)
a = torch.tensor([1.0, 2.0, 3.0])
W = torch.tensor([0.1, 0.2, 0.3], requires_grad=True)
b = torch.tensor(1.0, requires_grad=True)
y = W*a+b
z = torch.sum(y)
z.backward()
print(W.grad, b.grad) # dz/dW, dz/db
# dz/dW = (dz/dy).(dy/dW)
# dy/dW = a = [1.0, 2.0, 3.0]

# dz/db = (dz/dy).(dy/db) = 1. + 1. + 1. = 3.

tensor([1., 2., 3.]) tensor(3.)
.zero_()
Xóa gradient cũ trước vòng tiếp theo.

.reshape()
Giống với view nhưng an toàn hơn.
.squeeze()
Xóa các chiều có size = 1. Mục đích là loại bỏ chiều thừa không cần thiết. Cần gán vào một biến mới
Cú pháp:
x = torch.randn(1,3,1,5)

y = x.squeeze()
z = x.squeeze(2)
t = x.squeeze(3)
print(y.shape, z.shape, t.shape) # torch.Size([3, 5]) torch.Size([1, 3, 5]) torch.Size([1, 3, 1, 5])
.unsqueeze()
Dùng khi cần biến một tensor thành dạng có thêm nhiều chiều.
Cú pháp:
x = torch.tensor([1, 2, 3, 4, 5, 6])  # (6,)
x = x.unsqueeze(1)   # (6, 1)
x = x.unsqueeze(2)   # (6, 1, 1)
x = x.unsqueeze(3)   # giờ mới được: (6, 1, 1, 1)

argmax()
Lấy chỉ số của giá trị lớn nhất. Mục đích là lấy nhãn được dự đoán lớn nhất trong xác suất đầu ra.
item()
parameters()
.tolist() 
Chuyển tensor sang danh sách Python.
Cú pháp:
import torch

arr = torch.randn(2,)
print(arr.tolist()) # [2.347059488296509, 0.8164411783218384]
x = torch.tensor([[1.0, 2.0], [3.0, 4.0]])
list_x = x.tolist()
print(list_x)
.clone()
Tạo bản sao độc lập của tensor
Cú pháp:
import torch

a = torch.tensor([1, 2, 3], dtype=torch.float32)
b = a.clone()

b[0] = 999

print("a:", a)
print("b:", b)
a: tensor([1., 2., 3.])
b: tensor([999., 2., 3.])
.detach()
Cắt tensor khỏi graph tính đạo hàm
Cú pháp:
import torch

x = torch.tensor(2.0, requires_grad=True)
y = x * 3
z = y.detach()  # tách z khỏi graph

out = z * 5
out.backward()  # ❌ không thể tạo gradient cho x

print(x.grad) # None
Cộng, trừ, nhân, chia 
x = torch.tensor([1.0, 2.0])
y = torch.tensor([3.0, 4.0])

print(x + y)  # tensor([4., 6.])
print(x * y)  # Nhân từng phần tử: tensor([3., 8.])

Arange()
import torch

a = torch.arange(0, 10, 2)
print(a)
tensor([0, 2, 4, 6, 8])

Zeros()
self.bh = torch.zeros(3, requires_grad=True) # (hidden_dim, )

exp()
Tanh()
Stack()
Ghép (stack) nhiều tensor cùng shape lại thành 1 tensor lớn hơn, bằng cách thêm 1 dimension mới.
Cú pháp:
import torch

a = torch.tensor([1, 2, 3])
b = torch.tensor([4, 5, 6])
c = torch.tensor([7, 8, 9])

out = torch.stack([a, b, c])
print(out)
print(out.shape)
tensor([
 [1, 2, 3],
 [4, 5, 6],
 [7, 8, 9]
])
torch.Size([3, 3])
out = torch.stack([a, b, c], dim=1)
print(out)
print(out.shape) # Lần này là xếp theo chiều 1 → ma trận bị đảo trục.
tensor([
 [1, 4, 7],
 [2, 5, 8],
 [3, 6, 9]
])
torch.Size([3, 3])
Cat()
Random
rand()
Để tạo ma trận ngẫu nhiên.
import torch

li = torch.rand(1,10) # random 0 - 1
li1 = int(torch.rand(1).item()*10) # nhân 10 rồi ép kiểu
print(li)
print(li1)
tensor([[0.6769, 0.5901, 0.8615, 0.4698, 0.7670, 0.2347, 0.0153, 0.6552, 0.3026, 0.6311]])
8
x = torch.rand(5,3) # 5 hàng và 3 cột

randn_like()
Randn()
Khởi tạo ngẫu nhiên theo phân phối chuẩn (Normal distribution).
Cú pháp:
X = torch.randn(32, 5, 3, device=device) 
    • 32: batch size tức là 32 câu.
    • 5: độ dài mỗi senquence, mỗi câu gồm 5 token.
    • 3: mỗi token biểu diễn thành vector 3 chiều.
# Tạo 1 tensor 2x3 gồm các giá trị ngẫu nhiên ~ N(0, 1)
x = torch.randn(2, 3)
print(x)
tensor([[ 0.3272, -1.1845,  0.4821],
        [ 1.0063, -0.3278, -0.2205]])
Randint()
y = torch.randint(0, 8, (32,), device=device)
manual_seed()
Để cố định random của PyTorch
Cú pháp:
import torch

torch.manual_seed(42)

print(torch.randn(3))
print(torch.randint(0, 10, (3,)))
no_grad()
Trong quá trình dự đoán (inference), bạn không cần tính gradient nữa (vì không học nữa). Việc tắt gradient sẽ giúp giảm tốn bộ nhớ, tăng tốc độ, tránh sai sót do vô tình .backward() khi không cần.
Cú pháp: 
with torch.no_grad():
    # các câu lệnh không cần tính gradient ở đây
Cuda
device()
is_available()
Trả về True/False. True là máy tính có thể chạy gpu.
Cú pháp:
torch.cuda.is_available()
get_device_name()
Trả về tên của gpu đang sử dụng.
Cú pháp:
print(torch.cuda.get_device_name(0))
.to()
Thiết lập chế độ chạy GPU hay CPU.
Cú pháp:
import torch

device = torch.device("cuda" if torch.cuda.is_available() else 'cpu')
a = torch.tensor([1,2]).to(device)
print(a.device) # cuda:0
Utils
Data
Dataset
Là lớp đại diện cho toàn bộ dữ liệu. Tập ảnh huấn luyện (train images), Dữ liệu dạng bảng (CSV), Các file văn bản, Bất cứ loại dữ liệu nào bạn muốn đưa vào mô hình
Tại sao phải dùng Dataset:
Nếu bạn chỉ đọc file trực tiếp bằng cv2.imread() hay pandas.read_csv(), bạn sẽ phải tự quản lý việc chia batch, shuffle, và load dần vào GPU → rất rối. PyTorch tạo ra lớp Dataset để bạn chỉ cần định nghĩa 2 hàm quan trọng: 
    • __len__() → cho biết có bao nhiêu mẫu dữ liệu 
    • __getitem__(index) → khi cần lấy mẫu thứ index, thì làm thế nào để load nó. 
Còn việc lặp qua batch, chia batch, shuffle… sẽ do DataLoader lo.
Cú pháp:
import torch
from torch.utils.data import Dataset
import pandas as pd
from typing import List

class RealEstateDataset(Dataset):
    def __init__(self, 
        data_frame: pd.DataFrame, 
        features: List[str],
        label: List[str]) -> None:

        self.data = data_frame

        self.X = torch.tensor(
            self.data[features].to_numpy(), 
            dtype=torch.float32
        )
        self.y = torch.tensor(
            self.data[label].to_numpy(), 
            dtype=torch.float32
        )
    
    def __len__(self) -> int:
        return len(self.data)
    
    def __getitem__(self, idx) -> tuple:
        return self.X[idx], self.y[idx]
    
if __name__ == "__main__":
    data = {
        'size': [850, 900, 1200, 1500],
        'bedrooms': [2, 3, 3, 4],
        'age': [10, 15, 20, 5],
        'price': [200000, 250000, 300000, 350000]
    }

    df = pd.DataFrame(data)
    
    features = ['size', 'bedrooms', 'age']
    labels = ['price']

    dataset = RealEstateDataset(df, features, labels)
    print(f'Data length: {dataset.__len__()}')
    print(f'First sample: {dataset.__getitem__(0)}')
Data length: 4
First sample: (tensor([850.,   2.,  10.]), tensor([200000.]))
Nn
Để xây dựng mạng nơ ron nhanh chóng.
Sequential()
Khởi tạo mô hình mạng nơ ron
Cú pháp:
self.net = nn.Sequential(
            nn.Linear(input_size, 128),
            nn.ReLU(),
            nn.Linear(128, 64),
            nn.ReLU(),
            nn.Linear(64, num_classes)
        )
.train()
Bật chế độ training mode.

Module
Linear
Là lớp fully connected (FC).
Cú pháp: 
nn.Linear(in_features, out_features)
    • in_features: số chiều input
    • out_features: số chiều output (số class nếu phân loại)
conv2d
functional
import torch
import torch.nn.functional as F

# tensor đầu ra của mô hình
logits = torch.tensor([2.0, 1.0, 0.1])
probs = F.softmax(logits, dim=0)
print(probs)
print(probs.sum())  # Kiểm tra tổng = 1
Softmax()
import tensorflow as tf

logits = tf.constant([2.0, 1.0, 0.1])
probs = tf.nn.softmax(logits)
print(probs.numpy())
print(tf.reduce_sum(probs).numpy())

fc = nn.Linear(in_features=8, out_features=3)

x = torch.randn(2, 5, 8)  # batch 2, 5 bước, mỗi bước 8 chiều
y = fc(x)
print(y.shape)  # (2, 5, 3)

Embedding
Biểu diễn từ (hoặc số nguyên) dưới dạng vector liên tục có ý nghĩa ngữ nghĩa.
Giống kiểu “tra bảng tra cứu” để ánh xạ từ ID sang vector. 
Cú pháp: 
nn.Embedding(num_embeddings, embedding_dim)
    • num_embeddings: Số lượng từ trong từ vựng (vocab size)
    • embedding_dim: Số chiều của vector biểu diễn mỗi từ
embedding = nn.Embedding(num_embeddings=4, embedding_dim=5)

input_ids = torch.tensor([1, 2, 3])
output = embedding(input_ids)

print(output)
tensor([[-2.2608, 0.2584, 0.0430, 0.6564, 0.0903], [-0.0245, 1.9173, 1.0353, 1.4358, 0.1202], [ 0.7551, 1.0152, -0.4208, 0.5330, -0.3870]], grad_fn=<EmbeddingBackward0>)
RNN
Là một lớp để xử lý dữ liệu chuỗi: văn bản, dữ liệu thời gian, âm thanh. RNN ghi nhớ trạng thái trước đó và sử dụng nó để xử lý phần tử tiếp theo.
Cú pháp: torch.nn.RNN(input_size, hidden_size, num_layers=1, batch_first=False)
    • Input_size: Số chiều của mỗi phần tử trong chuỗi.
    • Hidden_size: Số chiều của trạng thái ẩn.
    • Num_layers: Số tầng (lớp RNN)
    • Batch_first: Nếu true, input có dạng (batch, seq_len, input_size)
import torch
import torch.nn as nn

x = torch.randn(2,5,4)
rnn = nn.RNN(input_size=4, hidden_size=6, batch_first=True)
out, hidden = rnn(x)

print(out)
print(hidden)
tensor([[[ 0.3732, -0.3084, -0.0086, 0.0545, -0.2229, -0.2923], [-0.4432, -0.5456, 0.3753, 0.4180, 0.4578, -0.2580], [-0.8133, -0.6375, -0.6581, -0.2354, 0.9065, 0.3951], [-0.2597, -0.8807, -0.5363, -0.5203, 0.7042, -0.4658], [-0.4765, -0.6938, -0.0969, -0.1936, 0.4945, 0.1496]], [[-0.6179, 0.5726, 0.5082, -0.2073, 0.2589, 0.5827], [ 0.5372, -0.8405, -0.4114, -0.0832, 0.4964, -0.6965], [-0.4667, -0.2090, 0.6394, 0.6679, 0.3059, -0.0806], [ 0.0017, 0.1926, 0.0041, 0.5061, 0.4831, 0.2032], [-0.1841, 0.4566, -0.5709, -0.3381, 0.2512, 0.5089]]], grad_fn=<TransposeBackward1>) tensor([[[-0.4765, -0.6938, -0.0969, -0.1936, 0.4945, 0.1496], [-0.1841, 0.4566, -0.5709, -0.3381, 0.2512, 0.5089]]], grad_fn=<StackBackward0>)
LSTM
GRU
ReLU()
Sigmoid()
self.sigmoid = nn.Sigmoid()
logits = self.w*X + self.b # linear
y_pred = self.sigmoid(logits) # sigmoid

Tanh()
tanh là lớp, phải gọi hàm kích hoạt

Softmax()
LeakyReLU
CrossEntropyLoss()
    • Là hàm mất mát (loss function) dùng trong các bài toán phân loại (classification). Nó đo mức độ khác nhau giữa xác suất dữ đoán của mô hình và nhãn thật.
    • Dùng khi đầu ra của mô hình là xác suất cho nhiều lớn (multi-class)
    • Nó kết kết hợp LogSoftmax + Negative Log Likelihood Loss (NLLLoss)
Cú pháp:
loss_fn = nn.CrossEntropyLoss()
loss = loss_fn(output, target)
    • Output: Tensor đầu ra từ mô hình (logits - chưa softmax), kích thước [batch_size, num_classes]
    • Target: tensor chứa nhãn thật, là chỉ số lớp (int), kích thước [batch_size]
out = torch.tensor([[2.0, 1.2, 1]])
target = torch.tensor([0])

loss_fn = nn.CrossEntropyLoss()
loss = loss_fn(out, target)
print(loss.item())
print(loss)
0.5973015427589417 tensor(0.5973)
BCELoss()
self.loss_fn = nn.BCELoss()
loss = self.loss_fn(y_pred, y)

MSELoss()
MLLLoss()
BCEWithLogitsLoss()
ModuleList()
ModuleDict
parameters()
Optim
Cần import torch.optim as optim
SGD()
    • SGD phù hợp khi:
        ◦ Dữ liệu lớn & nhiễu nhiều → SGD ổn định hơn. Các mô hình rất lớn (ví dụ ResNet, ViT, YOLO) thường ưu tiên SGD vì:
            ▪ Adam quá nhanh → dễ rơi vào cực trị kém (bad minima)
            ▪ SGD mượt hơn → tổng quát hoá tốt hơn (generalization)
            ▪ Deep Learning các mô hình lớn = thường dùng SGD + momentum
    • Ví dụ:
        ◦ esNet → SGD
        ◦ EfficientNet → SGD
        ◦ YOLO → SGD
    • Bài toán cần generalization mạnh
        ◦ SGD đôi khi cho kết quả test accuracy tốt hơn Adam.
        ◦ Khi muốn mô hình không “nhảy loạn”
        ◦ Adam điều chỉnh tốc độ theo từng tham số → đôi khi bước nhảy quá mạnh.
Kết luận: SGD tốt cho mô hình lớn, bài toán thị giác (CV), bài toán cần generalization.

Adam()
    • Để tạo trình tối ưu hóa (optimizer), cụ thể nó là một thuật toán giúp giảm loss nhanh và hiệu quả.
    • Adam phù hợp khi:
        ◦ Mô hình nhỏ, vừa, hoặc bài toán khó tối ưu
        ◦ Adam tự điều chỉnh learning rate cho từng tham số → hội tụ nhanh và rất tiện.
    • Ví dụ dùng Adam là hợp lý:
        ◦ NLP (transformer các phiên bản nhỏ)
        ◦ Bài toán regression nhỏ
        ◦ Bài toán phi tuyến, phức tạp
        ◦ Autoencoder, GAN
        ◦ Recommender systems
        ◦ RL
    • Khi mới thử nghiệm mô hình → Adam dễ ra kết quả hơn
        ◦ Thay đổi lr không cần tuning quá nhiều.
        ◦ Batch size nhỏ
        ◦ Adam rất hợp với batch nhỏ, vì:
        ◦ Mức nhiễu gradient lớn → Adam làm mượt tốt hơn
Kết luận: Adam tốt cho bài toán nhỏ, nhanh, exploratory, NLP, hoặc khi gradient nhiễu.
Cú pháp: 
torch.optim.Adam(model.parameters(), lr=learning_rate)
    • model.parameters(): Láy các tham số cần tối ưu từ mô hình.
    • lr: learning rate - tốc độ học.
import torch
import torch.nn as nn

model = nn.Linear(2,1)
optimizer = torch.optim.Adam(model.parameters(), lr=0.1)
print(optimizer)

AdamW()
RMSprop()
.zero_grad()
Trong PyTorch, mỗi lần gọi loss.backward(), gradient không bị reset, mà sẽ cộng dồn vào thuộc tính .grad của từng tham số. Vì gradient bị cộng dồn, nên bạn phải xóa gradient cũ trước khi tính gradient mới, nếu không tham số sẽ cập nhật sai.
Cú pháp:
optimizer.zero_grad()
.step()
Dùng để cập nhật trong số tự động
Cú pháp:
optimizer.step()
