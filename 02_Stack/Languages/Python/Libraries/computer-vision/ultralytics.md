Ultralytics
cần tải pip install ultralytics
YOLO() 
Cú pháp:
from ultralytics import YOLO
model = YOLO("yolov8n.pt")   # tải model YOLOv8 nano (nhẹ nhất)
    • Có thể thay thế bằng:
        ◦ "yolov8s.pt" (small)
        ◦ "yolov8m.pt" (medium)
        ◦ "yolov10n.pt" (YOLOv10)
        ◦ "yolov8n-seg.pt" (segmentation)
        ◦ "yolov8n-pose.pt" (pose estimation)
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

print(model)
# nó sẽ in ra cấu trúc nơ ron của YOLO
Model()
Cú pháp:
results = model(source="image.jpg", save=True, stream=True, device=) # đường dẫn có thể là ảnh hoặc video
    • source=’image.jpg’: đường dẫn ảnh
    • save=True: Lưu ảnh, False là không lưu
    • device: chỉ định chạy cpu hoặc gpu
boxes: ultralytics.engine.results.Boxes object
keypoints: ultralytics.engine.results.Keypoints object
masks: None
names: {0: 'person'}
obb: None
orig_img: array(...)
orig_shape: (443, 665)
path: '/home/thang/projects/nhan_dien/img/predict_1.jpg'
probs: None
save_dir: 'runs/pose/predict'
speed: {'preprocess': 3.722213999935775, 'inference': 140.20678599990788, 'postprocess': 245.47614899984183}]
results = model("image.jpg", save=True) # results = model("video.mp4", save=True)
results = model(0)  # webcam
.show()
    • Hiển thị ngay ảnh bằng GUI tích hợp. show() hiển thị trực tiếp (bằng cv2 hoặc thư viện mặc định). Không trả về dữ liệu hình ảnh.
    • Chỉ phù hợp khi:
        ◦ Bạn muốn xem nhanh
        ◦ Debug khi đang phát triển
    • Nhược điểm:
        ◦ Không lưu được ảnh (phải screenshot)
        ◦ Không linh hoạt
        ◦ Không dùng được trong server (không có GUI), Linux headless, notebook…
Cú pháp:
results = model("image.jpg", save=True)
for r in results: # vì results là một list kết quả nên phải dùng vòng lặp
    r.show()   # hiện ảnh có bounding box
.plot()
    • Trả về ảnh đã được vẽ kết quả (recommended trong code). plot() không hiển thị luôn. Nó trả về một numpy array chứa ảnh gốc + keypoints/box đã vẽ.
    • Dùng để:
        ◦ Lưu ảnh
        ◦ Gửi ảnh vào pipeline khác
        ◦ Hiển thị bằng thư viện bạn muốn (cv2, PIL…)
        ◦ Tối ưu trong ứng dụng thực tế
Cú pháp:
from ultralytics import YOLO
model = YOLO("yolov8n-pose.pt")
results = model("person.jpg")
results[0].plot()  # hiện ảnh với keypoint
.train()
from ultralytics import YOLO

model = YOLO("yolov8n.pt")

model.train(
    data="data.yaml",
    epochs=50,
    imgsz=640,
    batch=16
)
train: datasets/images/train
val: datasets/images/val

names:
  0: cat
  1: dog
.boxes
boxes là thuộc tính quan trọng nhất, nó chứa tất cả các hộp giới hạn (bounding boxes) và thông tin liên quan.
Cú pháp:
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

all_boxes = results[0].boxes
print(f"Tổng số đối tượng được phát hiện trong ảnh: **{len(all_boxes)}**")
Tổng số đối tượng được phát hiện trong ảnh: **8**
.cls
Trả về id của lớp. ví dụ {0: ‘person’} thì nếu giá trị cls là 0 thì lớp đó là person
Cú pháp:
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

all_boxes = results[0].boxes

for i, box in enumerate(all_boxes):   
    print(box.cls[0])
tensor(41., device='cuda:0')
tensor(66., device='cuda:0')
tensor(67., device='cuda:0')
tensor(62., device='cuda:0')
tensor(63., device='cuda:0')
tensor(67., device='cuda:0')
tensor(67., device='cuda:0')
tensor(67., device='cuda:0')
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

all_boxes = results[0].boxes

for box in all_boxes:   
    print(box.cls.item())
41.0
66.0
67.0
62.0
63.0
67.0
67.0
67.0
.conf
box.conf là tensor chứa điểm tin cậy (confidence score) của phát hiện
Cú pháp:
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

all_boxes = results[0].boxes

for i, box in enumerate(all_boxes):   
    print(box.conf[0])
tensor(0.9537, device='cuda:0')
tensor(0.9295, device='cuda:0')
tensor(0.9042, device='cuda:0')
tensor(0.8160, device='cuda:0')
tensor(0.5819, device='cuda:0')
tensor(0.4090, device='cuda:0')
tensor(0.3846, device='cuda:0')
tensor(0.2900, device='cuda:0')
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

for b in results[0].boxes:
    print(b.conf.shape)
torch.Size([1])
torch.Size([1])
torch.Size([1])
torch.Size([1])
torch.Size([1])
torch.Size([1])
torch.Size([1])
torch.Size([1])
.xyxy
box.xyxy là tensor chứa tọa độ (x_min, y_min, x_max, y_max)
Cú pháp:
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

xyxy = results[0].boxes.xyxy

for i, coord in enumerate(xyxy):   
    print(coord)
tensor([ 80.7958, 314.5251, 213.7577, 432.0266], device='cuda:0')
tensor([1.2202e-01, 2.4386e+02, 2.2782e+02, 3.7741e+02], device='cuda:0')
tensor([185.8370, 287.1443, 301.3015, 346.3632], device='cuda:0')
tensor([  0.3699,   0.3549, 354.3244, 227.1534], device='cuda:0')
tensor([598.0267, 170.3140, 795.4203, 272.7632], device='cuda:0')
tensor([748.8848, 210.8769, 851.9120, 291.7232], device='cuda:0')
tensor([334.5608, 342.5161, 445.7292, 422.4576], device='cuda:0')
tensor([761.8676, 211.8118, 851.4373, 275.6527], device='cuda:0')
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

for b in results[0].boxes:
    print(b.xyxy.shape)
torch.Size([1, 4])
torch.Size([1, 4])
torch.Size([1, 4])
torch.Size([1, 4])
torch.Size([1, 4])
torch.Size([1, 4])
torch.Size([1, 4])
torch.Size([1, 4])
.data
.names & .names[]
.names là một từ điển (dictionary) tích hợp sẵn trong mô hình, ánh xạ ID lớp (class ID) sang tên lớp.
Cú pháp:
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

print(f'tổng số lớp mô hình nhận diện {len(model.names)}')
print(f'các lớp mô hình: {model.names}')
for i in range(len(results)):
    print(f'tên lớp có id {i} là: {model.names[i]}')
tổng số lớp mô hình nhận diện 80
các lớp mô hình: {0: 'person', 1: 'bicycle', 2: 'car', 3: 'motorcycle', 4: 'airplane', 5: 'bus', 6: 'train', 7: 'truck', 8: 'boat', 9: 'traffic light', 10: 'fire hydrant', 11: 'stop sign', 12: 'parking meter', 13: 'bench', 14: 'bird', 15: 'cat', 16: 'dog', 17: 'horse', 18: 'sheep', 19: 'cow', 20: 'elephant', 21: 'bear', 22: 'zebra', 23: 'giraffe', 24: 'backpack', 25: 'umbrella', 26: 'handbag', 27: 'tie', 28: 'suitcase', 29: 'frisbee', 30: 'skis', 31: 'snowboard', 32: 'sports ball', 33: 'kite', 34: 'baseball bat', 35: 'baseball glove', 36: 'skateboard', 37: 'surfboard', 38: 'tennis racket', 39: 'bottle', 40: 'wine glass', 41: 'cup', 42: 'fork', 43: 'knife', 44: 'spoon', 45: 'bowl', 46: 'banana', 47: 'apple', 48: 'sandwich', 49: 'orange', 50: 'broccoli', 51: 'carrot', 52: 'hot dog', 53: 'pizza', 54: 'donut', 55: 'cake', 56: 'chair', 57: 'couch', 58: 'potted plant', 59: 'bed', 60: 'dining table', 61: 'toilet', 62: 'tv', 63: 'laptop', 64: 'mouse', 65: 'remote', 66: 'keyboard', 67: 'cell phone', 68: 'microwave', 69: 'oven', 70: 'toaster', 71: 'sink', 72: 'refrigerator', 73: 'book', 74: 'clock', 75: 'vase', 76: 'scissors', 77: 'teddy bear', 78: 'hair drier', 79: 'toothbrush'}
tên lớp có id 0 là: person
Predict()
Hàm predict là hàm cốt lõi để chạy suy luận (inference) trên ảnh, video hoặc luồng dữ liệu theo thời gian thực.
Cú pháp:
results = model.predict(source, classes=[] stream=False, conf=0.25, iou=0.7, save=False…)
    • source:"Đầu vào (ảnh, video, thư mục ảnh, URL, luồng webcam, v.v.). str, Path, list, np.ndarray",
    • classes               :Dùng để chỉ định đối tượng nào sẽ được detect. tham số truyền vào là một mảng
    • conf: Ngưỡng độ tin cậy tối thiểu để chấp nhận một phát hiện – float - mặc định là 0.25
    • iou: Ngưỡng IOU (Intersection over Union) cho Non-Maximum Suppression (NMS) – float mặc định là 0.7
    • stream,"Chế độ xử lý luồng dữ liệu (ví dụ: video/webcam). Nếu True, sẽ trả về một trình tạo (generator).",bool,False,Không
    • save: Lưu kết quả suy luận (ảnh/video có hộp giới hạn) vào thư mục runs/detect/predict – bool - mặc định là False
    • show,Hiển thị kết quả trong một cửa sổ Pop-up.,bool,False,Không
    • device=’cuda’: thiết lập chạy trên gpu
from ultralytics import YOLO
import cv2

model = YOLO('weights/yolov8n.pt')

results_list = model.predict(
    source='data/images/many-objects.jpeg',
    conf=0.5,
    save=False
)

result = results_list[0]

total_detections = len(result.boxes)
print(f'tổng detect {total_detections}')

annotated_img = result.plot()

cv2.imshow("Demo", annotated_img)
cv2.waitKey(1)

if total_detections > 0:
        first_box = result.boxes[0]
        cls_id = int(first_box.cls[0].item())
        conf = first_box.conf[0].item()
        obj_name = model.names[cls_id]
        print(f"  -> Phát hiện đầu tiên: **{obj_name}** | Conf: **{conf:.2f}**")
tổng detect 5
  -> Phát hiện đầu tiên: **cup** | Conf: **0.95**
from ultralytics import YOLO
import cv2

model = YOLO('weights/yolov8n.pt')

results = model.predict(
    source='data/images/many-objects.jpeg',
    conf=0.5,
    save=False,
    device='cuda'
)
print(results)
boxes: ultralytics.engine.results.Boxes object
keypoints: None
masks: None
names: {0: 'person', 1: 'bicycle', 2: 'car', 3: 'motorcycle', 4: 'airplane', 5: 'bus', 6: 'train', 7: 'truck', 8: 'boat', 9: 'traffic light', 10: 'fire hydrant', 11: 'stop sign', 12: 'parking meter', 13: 'bench', 14: 'bird', 15: 'cat', 16: 'dog', 17: 'horse', 18: 'sheep', 19: 'cow', 20: 'elephant', 21: 'bear', 22: 'zebra', 23: 'giraffe', 24: 'backpack', 25: 'umbrella', 26: 'handbag', 27: 'tie', 28: 'suitcase', 29: 'frisbee', 30: 'skis', 31: 'snowboard', 32: 'sports ball', 33: 'kite', 34: 'baseball bat', 35: 'baseball glove', 36: 'skateboard', 37: 'surfboard', 38: 'tennis racket', 39: 'bottle', 40: 'wine glass', 41: 'cup', 42: 'fork', 43: 'knife', 44: 'spoon', 45: 'bowl', 46: 'banana', 47: 'apple', 48: 'sandwich', 49: 'orange', 50: 'broccoli', 51: 'carrot', 52: 'hot dog', 53: 'pizza', 54: 'donut', 55: 'cake', 56: 'chair', 57: 'couch', 58: 'potted plant', 59: 'bed', 60: 'dining table', 61: 'toilet', 62: 'tv', 63: 'laptop', 64: 'mouse', 65: 'remote', 66: 'keyboard', 67: 'cell phone', 68: 'microwave', 69: 'oven', 70: 'toaster', 71: 'sink', 72: 'refrigerator', 73: 'book', 74: 'clock', 75: 'vase', 76: 'scissors', 77: 'teddy bear', 78: 'hair drier', 79: 'toothbrush'}
obb: None
orig_img: array([[[ 45,  38,  35],
        [ 45,  38,  35],
        [ 47,  40,  37],
        ...,
        [100,  94,  95],
        [ 99,  93,  94],
        [ 99,  93,  94]]], dtype=uint8)
orig_shape: (482, 860)
path: '/home/thang/projects/Test/data/images/many-objects.jpeg'
probs: None
save_dir: 'runs/detect/predict'
speed: {'preprocess': 3.1937180001477827, 'inference': 126.71867700009898, 'postprocess': 228.35321700040367}]
.tolist()