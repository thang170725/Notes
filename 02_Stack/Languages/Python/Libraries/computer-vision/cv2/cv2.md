- [__version__](#version)
- [imread()](#imread)
- [lỗi vì đang sử dụng cv2.IMREAD\_GRAYSCALE tức là ảnh chỉ có một kênh màu (đen trắng). Trong trường hợp đó image.shape chỉ trả về 2 giá trị là height và width](#lỗi-vì-đang-sử-dụng-cv2imread_grayscale-tức-là-ảnh-chỉ-có-một-kênh-màu-đen-trắng-trong-trường-hợp-đó-imageshape-chỉ-trả-về-2-giá-trị-là-height-và-width)
- [Hình ảnh sau 2 giây sẽ bị mất](#hình-ảnh-sau-2-giây-sẽ-bị-mất)
- [bạn không tự động thấy ảnh từ camera. Bạn phải liên tục lấy ảnh từ webcam – và mỗi lần chụp ra tại một thời điểm, người ta gọi là một frame (giống như một khung hình trong video)](#bạn-không-tự-động-thấy-ảnh-từ-camera-bạn-phải-liên-tục-lấy-ảnh-từ-webcam--và-mỗi-lần-chụp-ra-tại-một-thời-điểm-người-ta-gọi-là-một-frame-giống-như-một-khung-hình-trong-video)
- [webcam là nguồn video, và video thực ra là nhiều ảnh nối tiếp nhau gọi là các frame](#webcam-là-nguồn-video-và-video-thực-ra-là-nhiều-ảnh-nối-tiếp-nhau-gọi-là-các-frame)
- [1. Định nghĩa hàm callback xử lý sự kiện chuột](#1-định-nghĩa-hàm-callback-xử-lý-sự-kiện-chuột)
- [2. Tạo một ảnh nền đen (512x512 pixel)](#2-tạo-một-ảnh-nền-đen-512x512-pixel)
- [3. Tạo cửa sổ và đặt tên cho nó (rất quan trọng)](#3-tạo-cửa-sổ-và-đặt-tên-cho-nó-rất-quan-trọng)
- [4. Gắn hàm callback vào cửa sổ đã tạo](#4-gắn-hàm-callback-vào-cửa-sổ-đã-tạo)
- [5. Vòng lặp chính để giữ cửa sổ mở](#5-vòng-lặp-chính-để-giữ-cửa-sổ-mở)
- [1. Tọa độ 4 điểm góc của sân trên ảnh gốc (ảnh nghiêng)](#1-tọa-độ-4-điểm-góc-của-sân-trên-ảnh-gốc-ảnh-nghiêng)
- [Thứ tự: Top-Left, Top-Right, Bottom-Right, Bottom-Left](#thứ-tự-top-left-top-right-bottom-right-bottom-left)
- [2. Tọa độ 4 điểm tương ứng bạn muốn hiển thị trên ảnh mới (hình chữ nhật)](#2-tọa-độ-4-điểm-tương-ứng-bạn-muốn-hiển-thị-trên-ảnh-mới-hình-chữ-nhật)
- [Giả sử ta muốn kết quả là ảnh 300x500](#giả-sử-ta-muốn-kết-quả-là-ảnh-300x500)
- [3. Tính ma trận biến đổi M](#3-tính-ma-trận-biến-đổi-m)
- [4. Áp dụng ma trận M để biến đổi ảnh (warp)](#4-áp-dụng-ma-trận-m-để-biến-đổi-ảnh-warp)
- [Giả sử 'img' là ảnh đầu vào của bạn](#giả-sử-img-là-ảnh-đầu-vào-của-bạn)
- [result = cv2.warpPerspective(img, M, (width, height))](#result--cv2warpperspectiveimg-m-width-height)
- [--- Bước 1: Giả lập ma trận M (thực tế bạn lấy từ getPerspectiveTransform) ---](#----bước-1-giả-lập-ma-trận-m-thực-tế-bạn-lấy-từ-getperspectivetransform----)
- [Tọa độ 4 góc sân trên Camera (ảnh bị nghiêng)](#tọa-độ-4-góc-sân-trên-camera-ảnh-bị-nghiêng)
- [Tọa độ 4 góc sân trên sơ đồ 2D (hình chữ nhật chuẩn)](#tọa-độ-4-góc-sân-trên-sơ-đồ-2d-hình-chữ-nhật-chuẩn)
- [--- Bước 2: Tọa độ một điểm cụ thể cần map (ví dụ: Quả cầu) ---](#----bước-2-tọa-độ-một-điểm-cụ-thể-cần-map-ví-dụ-quả-cầu----)
- [Giả sử quả cầu đang ở tọa độ (300, 400) trên frame camera](#giả-sử-quả-cầu-đang-ở-tọa-độ-300-400-trên-frame-camera)
- [Chuyển điểm về định dạng mảng 3 chiều (N, 1, 2)](#chuyển-điểm-về-định-dạng-mảng-3-chiều-n-1-2)
- [--- Bước 3: Sử dụng perspectiveTransform ---](#----bước-3-sử-dụng-perspectivetransform----)
- [Lấy kết quả x, y mới](#lấy-kết-quả-x-y-mới)
- [--- Bonus: Map nhiều điểm cùng lúc ---](#----bonus-map-nhiều-điểm-cùng-lúc----)
- [Nếu bạn có cả tọa độ cầu và 2 người chơi](#nếu-bạn-có-cả-tọa-độ-cầu-và-2-người-chơi)
- [ảnh được lưu dưới dạng mảng numpy 2d](#ảnh-được-lưu-dưới-dạng-mảng-numpy-2d)
- [chiều cao: y2 – y1](#chiều-cao-y2--y1)
- [chiều rộng: x2 – x1](#chiều-rộng-x2--x1)
- [Lấy ra ma trận 3x3 chữa giá trị cường độ của màu đỏ](#lấy-ra-ma-trận-3x3-chữa-giá-trị-cường-độ-của-màu-đỏ)
- [code này để hiển thị hình ảnh và bấm phím n để thoát hình ảnh](#code-này-để-hiển-thị-hình-ảnh-và-bấm-phím-n-để-thoát-hình-ảnh)
- [nếu không có vòng lặp while thì chương trình chỉ bắt kết quả đúng một lần từ bàn phím rồi sau đó kết thúc chương trình, hình ảnh sẽ tự động tắt khi hàm main() kết thúc kể cả có bấm đúng phím hay không](#nếu-không-có-vòng-lặp-while-thì-chương-trình-chỉ-bắt-kết-quả-đúng-một-lần-từ-bàn-phím-rồi-sau-đó-kết-thúc-chương-trình-hình-ảnh-sẽ-tự-động-tắt-khi-hàm-main-kết-thúc-kể-cả-có-bấm-đúng-phím-hay-không)
- [vòng lặp while để giữ cho chương trình luôn chạy đến khi nào bấm đúng phím ‘n’ thì mới thôi.](#vòng-lặp-while-để-giữ-cho-chương-trình-luôn-chạy-đến-khi-nào-bấm-đúng-phím-n-thì-mới-thôi)
- [Cắt giá trị vượt giới hạn (0-255)](#cắt-giá-trị-vượt-giới-hạn-0-255)
- [Hiển thị](#hiển-thị)
- [](#)
- [blur() \& GaussianBlur()](#blur--gaussianblur)
- [(11,11) là độ mờ, số càng lớn mờ càng nhiều, số này phải là số lẻ](#1111-là-độ-mờ-số-càng-lớn-mờ-càng-nhiều-số-này-phải-là-số-lẻ)
- [cvtColor()](#cvtcolor)
  - [chuyển ảnh màu sang ảnh đen trắng](#chuyển-ảnh-màu-sang-ảnh-đen-trắng)
- [giống hiệu ứng nét bút chì](#giống-hiệu-ứng-nét-bút-chì)
- [làm sắc nét ảnh](#làm-sắc-nét-ảnh)

---

- OpenCV để xử lý hình ảnh và nó hỗ trợ vô số các thuật toán liên quan đến lĩnh vực thị giác máy tính và lĩnh vực học máy. Nó có thể sử dụng card đồ họa (GPU) để xử lý nhằm tăng tốc độ xử lý.
- Cần pip install opencv-python, import cv2

# __version__
import cv2
print(cv2.__version__)
4.11.0
Đọc và hiển thị
# imread()
Được sử dụng để đọc một hình ảnh từ ổ đĩa và lưu nó dưới dạng một mảng NumPy để xử lý trong các ứng dụng xử lý ảnh.
**Syn**
```bash
cv2.imread(filename, flags)
- Filename: Đường dẫn đến ảnh (có thể là tuyệt đối hoặc tương đối).
- Flags: Chế độ đọc ảnh, mặc định là cv2.IMREAD_COLOR
    + cv2.IMREAD_COLOR (hoặc 1): Đọc ảnh màu bỏ kênh anpha.
    + cv2.IMREAD_GRAYSCALE (hoặc 0): Đọc ảnh ở dạng grayscale (đen trắng).
    + cv2.IMREAD_UNCHANGED (hoặc -1): Giữ nguyên ảnh, kể cả kênh alpha nếu có.
```

.shape
Là một thuộc tính của mảng ảnh NumPy vì cv2.imread() trả về một numpy.ndarray. Nó cho biết kích thức và một số kênh màu.
Trả về 3 giá trị height, width, depth
    • h – chiểu cao của ảnh, pixels
    • w – chiều rộng của ảnh, pixels
    • 3 – số kênh màu (BGR)
    • 4 – số kênh màu + alpha (BGR + trong suốt)
Cú pháp:
import cv2
def main():
    # Load an image
    image = cv2.imread('night.jpg', cv2.IMREAD_GRAYSCALE)
    # Check if the image was loaded successfully
    if image is None:
        print("Error: Could not load image.")
        return
    else:
        h, w, c = image.shape
        print("kích thước ảnh:", image.shape)
        print("Chiều cao:", h)
        print("Chiều rộng:", w)
        print("Số kênh màu:", c)
        return
main()
ValueError: not enough values to unpack (expected 3, got 2)
# lỗi vì đang sử dụng cv2.IMREAD_GRAYSCALE tức là ảnh chỉ có một kênh màu (đen trắng). Trong trường hợp đó image.shape chỉ trả về 2 giá trị là height và width
import cv2
def main():
    # Load an image
    image = cv2.imread('night.jpg')
    # Check if the image was loaded successfully
    if image is None:
        print("Error: Could not load image.")
        return
    else:
        h, w, c = image.shape
        print("kích thước ảnh:", image.shape)
        print("Chiều cao:", h)
        print("Chiều rộng:", w)
        print("Số kênh màu:", c)
        return
main()
kích thước ảnh: (719, 1200, 3)
Chiều cao: 719
Chiều rộng: 1200
Số kênh màu: 3
Imshow()
Để hiển thị hình ảnh.
Cú pháp: 
cv2.imshow(<mô tả>, <attribute>)
import cv2
def main():
    # Load an image
    image = cv2.imread('night.jpg', cv2.IMREAD_GRAYSCALE)
    # Check if the image was loaded successfully
    if image is None:
        print("Error: Could not load image.")
    # Display the image in a window
    cv2.imshow('Ảnh hạ long', image)

    # Wait for a key press and close the window
    cv2.waitKey(0)
    cv2.destroyAllWindows()
main()
WaitKey()
    • Được sử dụng khi hiển thị hình ảnh hoặc video để tạm dừng chương trình và chờ người dùng nhấn phím.
    • Để giữ cửa sổ hiển thị ảnh hoặc video không bị tắt ngay lập tức.
Cú pháp: 
cv2.waitKey(0)
    • 0: Dừng vô thời hạn – chờ đến khi người dùng bấm phím thì chương trình mới thoát. (1000: Dừng 1 giây). Đối với video waitkey để càng lớn tốc độ video sẽ càng chậm
import cv2
def main():
    # Load an image
    image = cv2.imread('night.jpg', cv2.IMREAD_GRAYSCALE)
    # Check if the image was loaded successfully
    if image is None:
        print("Error: Could not load image.")
    # Display the image in a window
    cv2.imshow('Ảnh hạ long', image)

    # Wait for a key press and close the window
    cv2.waitKey(2000)
    cv2.destroyAllWindows()
main()
# Hình ảnh sau 2 giây sẽ bị mất
DestroyAllWindows()
Dùng để đóng tất cả các của sổ hiểu thị hình ảnh do OpenCV tạo ra. Giúp giải phóng bộ nhớ và tránh treo chương trình.
Cú pháp: 
cv2.destroyAllWidows()
import cv2
def main():
    # Load an image
    image = cv2.imread('night.jpg')
    # Check if the image was loaded successfully
    if image is None:
        print("Error: Could not load image.")
    # Display the image in a window
    cv2.imshow('Ảnh hạ long', image)

    # Wait for a key press and close the window
    cv2.waitKey(0)
    cv2.destroyAllWindows()
main()
resize()
Cú pháp: 
cv2.resize(
   src=frame, 
   dsize=(300, 200),
)
    • src: Ảnh gốc
    • dsize: Kích thước đích dưới dạng (width, height) (bắt buộc nếu không dùng fx, fy)
import cv2

image = cv2.imread('night.jpg')
if image is None:
    print("Không thể tải ảnh")
else:
    print("Kích thước gốc:", image.shape)

    resized = cv2.resize(image, (400, 300))  # Resize về 400x300
    print("Kích thước mới:", resized.shape)

    cv2.imshow("Resized Image", resized)
    cv2.waitKey(0)
    cv2.destroyAllWindows()

Bài tập
resize giữ tỉ lệ khi biết chiều rộng, tự tính chiều cao
import cv2

h, w = frame.shape[:2]
new_w = 640
new_h = int(h * new_w / w)

resized = cv2.resize(frame, (new_w, new_h))
resize giữ tỉ lệ khi biết chiều cao, tự tính chiều rộng
new_h = 480
new_w = int(w * new_h / h)

resized = cv2.resize(frame, (new_w, new_h))

NameWindow()
Tạo ra một cửa số có tên.
Cú pháp:
cv2.namedWindow("Get Tọa Độ")

ResizeWindow()
Dùng để thay đổi kích thước cửa sổ hiển thị 
Cú pháp:
import cv2

img = cv2.imread("image.jpg")

cv2.namedWindow("window", cv2.WINDOW_NORMAL)   # cho phép resize
cv2.resizeWindow("window", 800, 600)           # set kích thước cửa sổ

cv2.imshow("window", img)
cv2.waitKey(0)
cv2.destroyAllWindows()

VideoCapture() & .read() & .release()
Là một class được sử dụng để, mở video từ file (mp4, avi, …) truy cập webcam hoặc camera khác để chụp ảnh hoặc quay video trên thời gian thực.
Cú pháp: 
cv2.VideoCapture(source)
source có thể là:
    • Một số nguyên: 0, 1, 2, ... → chỉ số của webcam (0 là webcam mặc định).
    • Một chuỗi đường dẫn: "video.mp4" → mở video từ file.

import cv2

def main():
cap = cv2.VideoCapture(0)

    if not cap.isOpened():
        print("Không thể mở webcam")
        return
    else:
        while True:
            ret, frame = cap.read()
            if not ret:
                break
            cv2.imshow("Webcam", frame)
            if cv2.waitKey(25) & 0xFF == ord('q'):
                break
    cap.release()
    cv2.destroyAllWindows()
main()
# bạn không tự động thấy ảnh từ camera. Bạn phải liên tục lấy ảnh từ webcam – và mỗi lần chụp ra tại một thời điểm, người ta gọi là một frame (giống như một khung hình trong video)
# webcam là nguồn video, và video thực ra là nhiều ảnh nối tiếp nhau gọi là các frame
Vẽ hình và viết chữ
Circle()
cv2.circle(
   img=frame, 
   center=(x, y), 
   radius=5, 
   color=(0, 0, 255), 
   thickness=-1
   lineType,
   shift
)
    • Thickness:     Độ dày đường viền. Nếu để số âm (ví dụ: -1), hình tròn sẽ được tô đặc. 2 hoặc -1
Rectangle()
Dùng để vẽ hình chữ nhật
Cú pháp:
cv2.rectangle(
    frame,
    pt1=(x1, y1),
    pt2=(x2, y2),
    color=(0, 255, 0),
    thickness=2
)
PutText()
cv2.putText(img, text, org, fontFace, fontScale, color, thickness, lineType)
    • img	Ảnh hoặc khung hình (frame) bạn muốn vẽ lên.
    • text	Nội dung chữ (Kiểu String). Lưu ý: OpenCV mặc định không viết được tiếng Việt có dấu.
    • org	Tọa độ điểm bắt đầu (góc dưới bên trái của chữ) dạng (x, y).
    • fontFace	Loại font chữ (Ví dụ: cv2.FONT_HERSHEY_SIMPLEX, cv2.FONT_HERSHEY_COMPLEX).
    • fontScale	Tỷ lệ kích thước chữ (Số thực, ví dụ: 1.0, 0.5).
    • color	Màu sắc theo hệ BGR (ví dụ: (0, 255, 0) là màu xanh lá).
    • thickness	Độ dày nét chữ (Số nguyên).
    • lineType	Loại đường nét. Nên dùng cv2.LINE_AA (Anti-Aliased) để chữ mịn, không bị răng cưa.
SetMouseCallback()
EVENT_LBUTTONDOWN
Là một hằng số đại diện cho sự kiện nhấn chuột trái. Để sử dụng nó, bạn cần thiết lập một hàm gọi là Callback function và gắn nó vào một cửa sổ hiển thị bằng lệnh cv2.setMouseCallback.
Cách thức hoạt động:
Quy trình thực hiện gồm 3 bước chính:
    • Định nghĩa hàm Callback: Hàm này sẽ tự động được gọi mỗi khi có sự kiện chuột xảy ra.
    • Tạo một cửa sổ: Phải có một cửa sổ với tên cụ thể (ví dụ: "Image Window").
    • Kết nối: Dùng cv2.setMouseCallback("Tên cửa sổ", tên_hàm_callback) để liên kết.
Cú pháp:
import cv2
import numpy as np

# 1. Định nghĩa hàm callback xử lý sự kiện chuột
def handle_mouse_click(event, x, y, flags, param):
    # Kiểm tra xem sự kiện có phải là nhấn chuột trái không
    if event == cv2.EVENT_LBUTTONDOWN:
        print(f"Bạn vừa click vào tọa độ: x={x}, y={y}")
        
        # Vẽ một hình tròn nhỏ màu xanh tại điểm click
        # (img, center, radius, color, thickness)
        cv2.circle(img, (x, y), 5, (255, 0, 0), -1)
        
        # Cập nhật lại hình ảnh hiển thị
        cv2.imshow("Mouse Event Demo", img)

# 2. Tạo một ảnh nền đen (512x512 pixel)
img = np.zeros((512, 512, 3), np.uint8)

# 3. Tạo cửa sổ và đặt tên cho nó (rất quan trọng)
cv2.namedWindow("Mouse Event Demo")

# 4. Gắn hàm callback vào cửa sổ đã tạo
cv2.setMouseCallback("Mouse Event Demo", handle_mouse_click)

print("Hướng dẫn: Click chuột trái lên cửa sổ ảnh để vẽ điểm.")
print("Nhấn phím 'q' hoặc 'Esc' để thoát.")

# 5. Vòng lặp chính để giữ cửa sổ mở
while True:
    cv2.imshow("Mouse Event Demo", img)
    
    # Đợi phím bấm (20ms)
    key = cv2.waitKey(20) & 0xFF
    if key == ord('q') or key == 27: # Thoát khi nhấn 'q' hoặc Esc
        break

cv2.destroyAllWindows()


Bài tập
Lấy tọa độ điểm bằng frame đầu của video
import cv2

points = []

def get_coords(event, x, y, flags, param):
    if event == cv2.EVENT_LBUTTONDOWN:
        points.append((x, y))
        print(f"Click: {x}, {y}")

cap = cv2.VideoCapture("video.mp4")

cv2.namedWindow("Video")
cv2.setMouseCallback("Video", get_coords)

while True:
    ret, frame = cap.read()
    if not ret:
        break

    # vẽ điểm đã click
    for p in points:
        cv2.circle(frame, p, 5, (0, 0, 255), -1)

    cv2.imshow("Video", frame)

    if cv2.waitKey(30) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
import cv2

points = []

def get_coords(event, x, y, flags, param):
    if event == cv2.EVENT_LBUTTONDOWN:
        points.append((x, y))
        print(points)

cap = cv2.VideoCapture("video.mp4")

ret, frame = cap.read()   # 👈 CHỈ đọc 1 frame
if not ret:
    print("Không đọc được video")
    exit()

cv2.namedWindow("Frame 0")
cv2.setMouseCallback("Frame 0", get_coords)

while True:
    show = frame.copy()

    for p in points:
        cv2.circle(show, p, 5, (0, 0, 255), -1)

    cv2.imshow("Frame 0", show)

    key = cv2.waitKey(1) & 0xFF
    if key == ord('q'):   # nhấn q để thoát
        break

cap.release()
cv2.destroyAllWindows()

print("Tọa độ cuối cùng:", points)

Polylines()
Dùng để vẽ đa giác
Cú pháp:
pts = np.array([
    [300, 700],
    [600, 400],
    [1200, 400],
    [1600, 700]
], np.int32)

cv2.polylines(frame, [pts], True, (255, 0, 0), 2)
FillPoly()
Dùng để tạo mask

mask = np.zeros(frame.shape[:2], dtype=np.uint8)
cv2.fillPoly(mask, [pts], 255)
bitwise_and()
Dùng để áp mask ROI

roi = cv2.bitwise_and(frame, frame, mask=mask)
PointPolygonTest()
Kiểm tra điểm có nằm trong ROI không. Dùng để: Check bbox center có trong ROI khôn

cx, cy = 500, 600
inside = cv2.pointPolygonTest(pts, (cx, cy), False)

if inside >= 0:
    print("Object inside ROI")
InRange()
ROI theo màu (nâng cao) Thường dùng cho:

Làn đường

Biển báo

Vạch kẻ

mask = cv2.inRange(hsv, lower, upper)
FindContours()
ROI dựa trên hình dạngDùng khi:

ROI không cố định

ROI sinh ra từ segmentation

contours, _ = cv2.findContours(mask, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
BoundingRect()
chuyển contour → ROI rectangle

x, y, w, h = cv2.boundingRect(cnt)
roi = frame[y:y+h, x:x+w]
GetPerspectiveTransform()
    • Dùng để tính toán một ma trận chuyển đổi kích thước 3×3 (gọi là ma trận biến đổi phối cảnh). 
    • Ma trận này cho phép bạn chuyển một vùng hình ảnh từ góc nhìn nghiêng (3D perspective) về một góc nhìn thẳng từ trên xuống (2D bird's-eye view).
Cú pháp:
M = cv2.getPerspectiveTransform(
   src, 
   dst
)
    • src: Mảng chứa tọa độ 4 điểm trên hình ảnh gốc (ảnh bị nghiêng). kiểu np.float32
    • dst: Mảng chứa tọa độ 4 điểm tương ứng trên hình ảnh đích (hình chữ nhật chuẩn).
    • M: Kết quả trả về là ma trận 3×3. kiểu np.float32
import cv2
import numpy as np

# 1. Tọa độ 4 điểm góc của sân trên ảnh gốc (ảnh nghiêng)
# Thứ tự: Top-Left, Top-Right, Bottom-Right, Bottom-Left
pts_src = np.array([
    [200, 150], [450, 150], 
    [550, 450], [100, 450]
], dtype="float32")

# 2. Tọa độ 4 điểm tương ứng bạn muốn hiển thị trên ảnh mới (hình chữ nhật)
# Giả sử ta muốn kết quả là ảnh 300x500
width, height = 300, 500
pts_dst = np.array([
    [0, 0], [width, 0], 
    [width, height], [0, height]
], dtype="float32")

# 3. Tính ma trận biến đổi M
M = cv2.getPerspectiveTransform(pts_src, pts_dst)

# 4. Áp dụng ma trận M để biến đổi ảnh (warp)
# Giả sử 'img' là ảnh đầu vào của bạn
# result = cv2.warpPerspective(img, M, (width, height))

print("Ma trận biến đổi M:")
print(M)

PerspectiveTransform()
    • Dùng để tính toán tọa độ mới của các điểm (tập hợp các điểm x, y).
    • Ví dụ: Trong bài toán sân cầu lông, hàm này cực kỳ hữu ích để bạn lấy tọa độ quả cầu hoặc vận động viên trên camera rồi chuyển nó thành tọa độ x,y trên sơ đồ sân 2D.
Cú pháp:
dst_points = cv2.perspectiveTransform(src_points, M)
    • src_points: Mảng các điểm cần chuyển đổi.
        ◦ Lưu ý cực kỳ quan trọng: Mảng này phải có cấu trúc 3 chiều với định dạng (N, 1, 2), trong đó N là số lượng điểm. Kiểu dữ liệu phải là float32.
    • M: Ma trận biến đổi 3×3 (đã tính được từ hàm cv2.getPerspectiveTransform).
    • dst_points: Kết quả trả về là tọa độ các điểm sau khi đã "trải phẳng" về 2D.
import cv2
import numpy as np

# --- Bước 1: Giả lập ma trận M (thực tế bạn lấy từ getPerspectiveTransform) ---
# Tọa độ 4 góc sân trên Camera (ảnh bị nghiêng)
src_corners = np.array([[100, 100], [500, 100], [600, 500], [0, 500]], dtype="float32")
# Tọa độ 4 góc sân trên sơ đồ 2D (hình chữ nhật chuẩn)
dst_corners = np.array([[0, 0], [610, 0], [610, 1340], [0, 1340]], dtype="float32")

M = cv2.getPerspectiveTransform(src_corners, dst_corners)

# --- Bước 2: Tọa độ một điểm cụ thể cần map (ví dụ: Quả cầu) ---
# Giả sử quả cầu đang ở tọa độ (300, 400) trên frame camera
ball_x, ball_y = 300, 400

# Chuyển điểm về định dạng mảng 3 chiều (N, 1, 2)
points_to_map = np.array([[[ball_x, ball_y]]], dtype="float32")

# --- Bước 3: Sử dụng perspectiveTransform ---
mapped_points = cv2.perspectiveTransform(points_to_map, M)

# Lấy kết quả x, y mới
new_x = mapped_points[0][0][0]
new_y = mapped_points[0][0][1]

print(f"Tọa độ gốc trên Camera: ({ball_x}, {ball_y})")
print(f"Tọa độ sau khi map vào sân 2D: ({new_x:.2f}, {new_y:.2f})")

# --- Bonus: Map nhiều điểm cùng lúc ---
# Nếu bạn có cả tọa độ cầu và 2 người chơi
many_points = np.array([
    [[300, 400]], # Quả cầu
    [[150, 450]], # Người chơi A
    [[450, 200]]  # Người chơi B
], dtype="float32")

mapped_many = cv2.perspectiveTransform(many_points, M)
print("\nDanh sách các điểm đã map:")
for i, pt in enumerate(mapped_many):
    print(f"Điểm {i+1}: {pt[0]}")
MinAreaRect()
Hàm này tìm một hình chữ nhật bao quanh có diện tích nhỏ nhất cho một tập hợp điểm. Khác với cv2.boundingRect (luôn thẳng đứng), minAreaRect có thể xoay theo hướng của vật thể.
Cú pháp:

.get()
Lấy kích thước của video
Cú pháp:
cap.get(input)
    • cv2.CAP_PROP_FPS: lấy ra tốc độ của video gốc
    • cv2.CAP_PROP_FRAME_WIDTH: lấy chiều rộng của video
    • cv2.CAP_PROP_FRAME_HEIGHT: Lấy chiều cao của video
import cv2

cap = cv2.VideoCapture('video/output.mp4')

width  = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))

print(height, width)

[]

import cv2
def main():
    # Load an image
    image = cv2.imread('night.jpg')
    # Check if the image was loaded successfully
    if image is None:
        print("Error: Could not load image.")
        return
    else:
        # lấy màu ở tọa độ (50, 50)
        b, g, r = image[50, 50]
        print(f"Pixel value at (50, 50): B={b}, G={g}, R={r}")
        return
main()
Pixel value at (50, 50): B=188, G=96, R=83
import cv2
def main():
    # Load an image
    image = cv2.imread('night.jpg')
    # Check if the image was loaded successfully
    if image is None:
        print("Error: Could not load image.")
        return
    else:
        imageCut = image[50:100, 1000:1500]
        cv2.imshow('Image Cut', imageCut)
        cv2.waitKey(0)
        cv2.destroyAllWindows()
        return
main()
# ảnh được lưu dưới dạng mảng numpy 2d
# chiều cao: y2 – y1
# chiều rộng: x2 – x1
red_values = img[0:3, 0:3, 2]
# Lấy ra ma trận 3x3 chữa giá trị cường độ của màu đỏ
Ví dụ
import cv2
def main():
    # Load an image
    image = cv2.imread('night.jpg', cv2.IMREAD_GRAYSCALE)
    # Check if the image was loaded successfully
    if image is None:
        print("Error: Could not load image.")
        return
    # Display the image in a window
    cv2.imshow('Image Ha Long Bay', image)

    while True:
        # Wait for a key press
        key = cv2.waitKey(0) & 0xFF
        # If 'q' is pressed, exit the loop
        if key == ord('n'):
            print("Exiting...")
            cv2.destroyAllWindows()
            break # Exit the loop and close the window
        else: print("you pressed:", chr(key))
main()
# code này để hiển thị hình ảnh và bấm phím n để thoát hình ảnh
# nếu không có vòng lặp while thì chương trình chỉ bắt kết quả đúng một lần từ bàn phím rồi sau đó kết thúc chương trình, hình ảnh sẽ tự động tắt khi hàm main() kết thúc kể cả có bấm đúng phím hay không
# vòng lặp while để giữ cho chương trình luôn chạy đến khi nào bấm đúng phím ‘n’ thì mới thôi.
Lưu ý: imshow() chỉ sử dụng dụng được chữ viết không dấu, không hỗ trợ hiển thị văn bản Unicode (tiếng việt) trực tiếp trong tiêu đề cửa sổ. Hàm imshow() chỉ hỗ trợ chuỗi ASCII. Tuy nhiên, bạn có thể khắc phục bằng cách tạo một cửa sổ riêng bằng thư viện khác như tkiner hoặc vẽ chữ tiếng việt trực tiếp lên ảnh bằng pillow (với font hỗ trợ unicode)
Cách tốt nhất là dùng pillow + cv2 để hiển thị hình ảnh với chữ tiếng việt.
Code thuần làm mờ ảnh
import numpy as np
import cv2
img = cv2.imread('anh3.jpg')
kernel = np.array([
    [1,2,1],
    [2,4,2],
    [1,2,1]
], dtype=np.float32)/16
h, w, c = img.shape
blurred = np.zeros_like(img)

for y in range(1,h-1):
    for x in range(1,w-1):
        for ch in range(3):
            region = img[y-1:y+2, x-1:x+2, ch]
            blurred[y,x,ch] = np.sum(region*kernel)
# Cắt giá trị vượt giới hạn (0-255)
blurred = np.clip(blurred, 0, 255).astype(np.uint8)

# Hiển thị
cv2.imshow('Original', img.astype(np.uint8))
cv2.imshow('Blurred', blurred)
cv2.waitKey(0)
cv2.destroyAllWindows()

# 
Dùng để làm mờ ảnh, cách hoạt động giống với gaussianBlur chỉ khác là ma trận kernel.
# blur() & GaussianBlur()
Đều dùng để làm mờ ảnh nhưng có những cách sử lý làm mờ khác nhau mà tác dụng cũng khác nhau
**GaussianBlur**
**Syn**
```bash
cv2.GaussianBlur(src=, ksize=, sigmaX=0)
- src: ảnh gốc (ảnh đầu vào).
- ksize: bộ lọc (kernel size), dạng (width, height), phải là số lẻ (ví dụ: (5,5)).
- sigmaX: độ lệch chuẩn theo trục X.
```
Cách hoạt động:
Giả sử chúng ta muốn tính giá trị của pixel tại vị trí (1,1), giá trị 60 trong ví dụ. Chúng ta sẽ đặt môt kernel 3x3 lên ma trận ảnh sao cho trung tâm của kernel đó trùng với pixel(1,1).
Các pixel xung quanh pixel (1,1) trong ma trận ảnh gốc sẽ là:

Bây giờ, chúng ta sẽ thực hiện phép tích chập:
Giá trị pixel mới tại (1,1) sẽ là: (10×0.0625)+(20×0.125)+(30×0.0625)+ (50×0.125)+(60×0.25)+(70×0.125)+ (90×0.0625)+(100×0.125)+(110×0.0625)
=0.625+2.5+1.875+ 6.25+15+8.75+ 5.625+12.5+6.875
=65
Vậy, giá trị pixel mới tại vị trí (1,1) trong ma trận kết quả sẽ là 65.
import cv2
anh = cv2.imread('anh1.jpg', -1)
blur = cv2.GaussianBlur(anh, (11,11), 0)
cv2.imshow("anh", blur)
cv2.waitKey(0)
cv2.destroyAllWindows()
# (11,11) là độ mờ, số càng lớn mờ càng nhiều, số này phải là số lẻ
MedianBlur()
    • Median là bộ loc giảm nhiễu, đặc biệt hiệu quả với “salt & pepper noise” nhiễu muối tiêu - tức là các điểm trắng/đen ngẫu nhiên.
Cách hoạt động:
    • Với mỗi pixel trong ảnh, ta lấy một vùng lân cận (3x3, 5x5, …)
    • sắp xếp tất cả cấc giá trị pixel trong vùng đó theo thứ tự.
    • Thay pixel trung tâm bằng giá trị median của vùng đó.
import cv2

img = cv2.imread('anh3.jpg')
cv2.imshow("original", img)

median = cv2.medianBlur(img, 5)
cv2.imshow("test", median)
cv2.waitKey(0)
cv2.destroyAllWindows()
Canny()
Là hàm dùng để phát hiện cạnh trong ảnh, rất phổ biến và hiệu quả.
Cú pháp: edges = cv2.Canny(image, threshold1, threshold2)
    • image: ảnh đầu vào (thường là ảnh xám – grayscale).
    • threshold1, threshold2: ngưỡng dưới và trên để xác định cạnh.
Các bước hoạt động:
    1. Làm mờ ảnh bằng bộ lọc gaussian: Giảm nhiễu, nhiễu có thể gây ra các cạnh giả.
    2. Tính toán gradient cường độ và hướng gradient: Xác định các vùng có sự thay đổi cường độ sáng lớn nhất.
    3. Làm trong hướng
    4. Loại bỏ các điểm không phải là cực đại cục bộ.
    5. Ngưỡng kép.
    6. Theo dõi cạnh bằng độ trễ
import cv2
anh = cv2.imread('anh1.jpg', 0)
edge = cv2.Canny(anh, 100,200)
cv2.imshow("anh", edge)
cv2.waitKey(0)
cv2.destroyAllWindows()

# cvtColor()
Là hàm dùng để chuyển đổi không gian màu của ảnh, ví dụ từ ảnh màu ảnh xám, RGB sang HSV, …
**Syn** 
```bash
dst = cv2.cvtColor(src, code)
- src: ảnh gốc (đầu vào).
- code: mã chuyển đổi màu, ví dụ:
    + cv2.COLOR_BGR2GRAY: chuyển ảnh từ BGR sang ảnh xám.
    + cv2.COLOR_BGR2RGB: chuyển từ BGR (mặc định OpenCV) sang RGB.
    + cv2.COLOR_BGR2HSV: chuyển từ BGR sang HSV.
```
**Ex**
```python
import cv2
anh = cv2.imread('anh1.jpg')
gray = cv2.cvtColor(anh, cv2.COLOR_BGR2GRAY)
cv2.imshow("anh", gray)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

## chuyển ảnh màu sang ảnh đen trắng
```python
import cv2
anh = cv2.imread('anh1.jpg')
gray = cv2.cvtColor(anh, cv2.COLOR_BGR2GRAY)
inv = 255 - gray
cv2.imshow("anh", inv)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

divide()
Dùng để chia từng pixel của 2 ảnh (hoặc ảnh với số) – hay dùng làm ảnh sáng, tạo hiệu ứng ảnh phác thảo (sketch).
Cú pháp: output = cv2.divide(src1, src2[, scale])
    • src1, src2: hai ảnh cùng kích thước.
    • scale (tùy chọn): hệ số nhân sau khi chia (mặc định = 1).
import cv2
gray = cv2.imread('anh1.jpg', 0)
inv = 255 - gray
blur = cv2.GaussianBlur(inv, (21,21), 0)
sketch = cv2.divide(gray, 255-blur, scale=256)
cv2.imshow("anh", sketch)
cv2.waitKey(0)
cv2.destroyAllWindows()
# giống hiệu ứng nét bút chì
filter2D()
Dùng để áp dụng để áp dụng bộ lọc tùy chỉnh lên ảnh – giúp làm mờ, làm sắc nét, phát hiện cạnh, …
Cú pháp: dst = cv2.filter2D(src, depth, kernel)
    • src: ảnh đầu vào.
    • depth: độ sâu ảnh đầu ra (-1 để giữ nguyên độ sâu ảnh gốc).
    • kernel: ma trận lọc (numpy array), ví dụ:
kernel = np.array([[0, -1, 0],
                   [-1, 5, -1],
                   [0, -1, 0]])
import cv2
import numpy as np
img = cv2.imread('anh1.jpg')
kernel = np.array([[0,-1,0],
                  [-1,5,-1],
                  [0,-1,0]])
sharrpend = cv2.filter2D(img, -1, kernel)
cv2.imshow("anh", sharrpend)
cv2.waitKey(0)
cv2.destroyAllWindows()
# làm sắc nét ảnh
bilateralFilter()
    • Bilateral filter (lọc song phương) là một bộ lọc phi tuyến tính, thực hiện làm mịn ảnh bằng cách kết hợp thông tịn không gian và cường độ màu (độ sáng) của điểm ảnh. Nó giữ cạnh rõ ràng vì:
        ◦ Không làm mờ các pixel có giá trị màu khác biệt lớn (ví dụ tại rìa cạnh).
        ◦ Chỉ làm mịn các pixel có màu tương tự và nằm gần nhau.
    • Hiểu đơn giản thì nó dùng một kernel có thể thay đổi giá trị. kernel này chứa
        ◦ Gaussian theo không gian -> đảm bảo các điểm gần được ưu tiên.
        ◦ Gaussian theo độ sáng -> loại bỏ các pixel có độ sáng quá khác biệt.
Cú pháp: cv2.bilateralFilter(src, d, sigmaColor, sigmaSpace)
    • src: Ảnh đầu vào.
    • d: Đường kính của pixel lân cận (cửa sổ) - ma trận kernel  
    • sigmaColor: Độ nhạy với khác biệt màu. Càng lớn thì càng mịn, bỏ qua sự khác biệt màu nhỏ. - kiểm soát mức độ quan tâm đến độ khác biệt màu sắc. 
    • sigmaSpace: Độ nhay với khoảng cách không gian. Càng lớn thì ảnh hưởng pixel xa hơn càng nhiều - Kiểm soát khaongr cách không gian trong kernel.
Dùng để:
    • Làm mịn ảnh mà vẫn giữ được cạnh sắc nét (khác với Gaussian blur).
    • Tiền xử lý cho nhận diện khuôn mặt, OCR, …
    • Trong làm đẹp ảnh (beautify filter).
    • Tách nền / foreground-background segmentation.
    • Trước khi phân đoạn ảnh (image segmentation)
Công thức:
I(filtered)​(i,j)=(1/W)(k,l∑​I(k,l))⋅Gs​(∥(k,l)−(i,j)∥)⋅Gr​(∣I(k,l)−I(i,j)∣)
Bài tập
Mở video từ file
import cv2

cap = cv2.VideoCapture(r'E:\video\Một chút chill.mp4')
if not cap.isOpened():
    print("Không thể mở video")
exit()

while True:
    ret, frame = cap.read()
    if not ret:
        print("Không thể đọc video hoặc đã hết video")
        break
    cv2.imshow(frame)
    if cv2.waitKey(25) & 0xFF == ord('q'):
        print("Bạn đã nhấn 'q', thoát...")
        break
cap.release()
cv2.destroyAllWindows()
