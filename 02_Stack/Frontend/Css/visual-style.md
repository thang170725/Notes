```bash
- Dùng để thiết kế hình dạng, phong cách cho box.
```
---
- [Box-shadow](#box-shadow)
- [backround-image](#backround-image)
- [Những website lấy icon](#những-website-lấy-icon)
---
# Box-shadow
```bash
- Để tạo bóng cho khối bao ngoài.
```
**Syn**
```bash
Box-shadow: h-shadow v-shadow blur spread color | inset | initial | inherit
Trong đó:
    • h-shadow: Vị trí bóng ngang so với chữ, số âm sẽ đẩy lên trên và số dương sẽ đẩy xuống dưới.
    • v-shadow: Vị trí bóng dọc so với chứ, số âm sẽ đẩy lui phía sau và số dương sẽ đẩy tới phía trước.
    • blur-radius: Độ nhòe của chữ bóng, tính bằng pixel.
    • spread: Kích thước của bóng tối.
    • color: Màu sắc của bóng, chấp nhận các inset: thay đổi bóng từ bên ngoài vào trong thay vì từ trong ra ngoài.
    • initial: Thiết lập giá trị mặc định.
    • inherit: Kế thừa giá trị từ thẻ HTML cha.
```

# backround-image
```bash
- Để Thiết lập hình nền.
```
Cú pháp:
background-image: value, …;
value:
    • url(‘ ’): Truyền vào một link của hình ảnh đó đuôi jpg hoặc png, …
    • conic-gradient: Thiết lập màu chuyển.
    • linear-gradient: Thiết lập màu chuyển.
linear-gradient
Để thiết lập dạng màu chuyển.
Cú pháp:
background: linear-gradient(direction | angles, color1, color2, …);

Trang web thiết kế dải màu linear-gradient đẹp mắt: https://webgradients.com/
repeating-linear-gradient
conic-gradient
Là một dạng chuyển đổi màu xoay quanh một điểm trung tâm.
Cú pháp: background-image: conic-gradient([fromangle] [at position,] color [degree], color [degree], ...);
Tạo hình bàn cờ
<body>
    <div></div>
  </body>

 body{
        background-image: repeating-conic-gradient(#5f0172 0 25%, #dfdb13 25% 50%);
        background-size: 384px 383px;
     }


Radial Gradients
Hiệu ứng màu chuyển lan tỏa ra tứ phía.
Cú pháp: background | background-image: radial-gradient(shape, size, at position, start-color, ..., last-color);
Lưu ý: Phải sử dụng đúng cấu trúc cú pháp trên.
Shape
Có 2 giá trị là ellipse (mặc định) và circle.
<div>Circle</div>
<div>Circle</div>

div:nth-child(1){
            width: 400px;
            height: 200px;
            background: radial-gradient(circle, #ff0000, #3399ff, #fffb00);
}
div:nth-child(2){
            width: 400px;
            height: 200px;
            background: radial-gradient(ellipse, #ff0000, #3399ff, #fffb00);
}
background-repeat 
Để Lặp hình nền hoặc không.
background-repeat: value;
value:
    • repeat-x: Lặp theo chiều ngang.
    • repeat-y: Lặp theo chiều dọc.
    • repeat: Lặp full block.
    • space: Lặp các góc của khối.
    • round: Lặp full khối.
    • no-repeat: Không lặp.
    • space-repeat: Lặp bỏ trống phần giữa theo chiều dọc.
    • round-space: Lặp bỏ trống phần giữa theo chiều ngang.
Border 
Để thiết lập đường viền cho phần tử. Là cách viết gộp của border-width, border-style, border-color.
Cú pháp:
border: border-width | border-style | border-color
border-style
Thiết lập kiểu viền cho khối bao quanh.
Cú pháp:
Border-style: value;
Value:
       dotted: Border sẽ hiển thị là những dấu chấm.
       dashed: Border sẽ hiển thị nét đứt.
       solid: Border sẽ hiển thị đường thẳng liền mạch.
       double: Border sẽ hiển thị 2 đường thẳng.
       groove: Border sẽ hiển thị dạng rãnh 3D.
       ridge: Border sẽ hiển thị dạng viền 3D.
       inset: Border sẽ hiển thị dạng viền trong 3D. 
       outset: Border sẽ hiển thị dạng viền đầu 3D. 
       none: Sẽ không có border.
       hidden: Border sẽ bị ẩn.

Nếu border-style có 4 giá trị thì giá trị lần lượt của nó là top, right, bottom, left.
Nếu border-style có 3 giá trị thì giá trị lần lượt của nó là top, right-left, bottom.
Nếu border-style có 2 giá trị thì giá trị lần lượt của nó là top-bottom, right-left.
Nếu border-style có 1 giá trị thì giá trị đó là top-right-bottom-left.
border-top-style
Thiết lập đường viền trên top.
border-right-style
Thiết lập đường viền bên phải.
border-bottom-style
Thiêt lập đường viền dưới.
border-left-style
Thiết lập đường viền bên trái.
Border-width
Thiết lập độ rộng cho viền.
giá trị:
    • number + đơn vị
    • thin, medium, thick.
Border-color
Thiết lập màu sắc cho viền.
    • Có 4 giá trị thì lần lượt thiết lập màu cho top, right, left, botttom.
    • Có 3 giá trị thì lần lượt thiết lập màu cho top, right-left, bottom.
    • Có 2 giá trị thì lần lượt thiết lập màu cho top-bottom, right-left.
    • Có 1 giá trị thì thiết lập màu cho top-right-left-bottom.
Ví dụ về border
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
        *{
            box-sizing: border-box;
        }
        div{
            width: 400px;
            height: 400px;
            background-color: #f00;
            border-top: 200px solid #abab;
            border-bottom: 200px solid transparent;
            border-left: 100px solid #000;
        }
    </style>
</head>
<body>
    <div></div>
</body>
</html>

border-image
Sử dụng hình ảnh làm đường viền của phần tử.
border-image-source
Chỉ định đường dẫn chứa hình ảnh được sử dụng để làm đường viền.
border-image-slice
Chỉ định cách cắt hình ảnh như thế nào.
border-image-width
Chỉ định độ rộng của hình ảnh.
border-image-outset
Chỉ định số lượng mà khu vực hình ảnh vượt qua ngoài cái hộp (box) của nó.
border-image-repeat
Chỉ định hình ảnh nên được lặp lại (repeated), làm tròn (rounded) hay kéo dài (stretched).
border-radius
Thiết lập bo góc cho viền. giá trị là number + đơn vị.
    • Nếu có 4 giá trị thì lần lượt là top-left, top-right, bottom-right, bottom-left.
    • Nếu có 3 giá trị thì lần lượt là top-left, toprihgt-bottom-left, bottom-right.
    • Nếu có 2 giá trị thì lần lượt là topleft-bottomright, topright-bottomleft.
    • Nếu có 1 giá trị thì giá trị đó là cả 4 góc.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
        body > div{
            position: relative;
            width: 100px;
            height: 100px;
            background-color: #000;
            border-radius: 10px / 20px;
        }
    </style>
</head>
<body>
    <div>
   </div>
</body>
</html>

Thiết lập góc bo tròn cho phần tử, sử dụng đường chéo để chỉ định bán kính bo tròn theo các góc khác nhau.
10px (bo tròn trên dưới)
20px (bo tròn trái phải)
Website tạo đường bo góc
    • Fancy-boder-radius
border-top-left-radius
Góc trên bên trái sẽ được uốn cong. Có thể truyền 1 hoặc 2 giá trị.
border-top-right-radius
Góc trên bên phải sẽ được uốn cong. Có thể truyền 1 hoặc 2 giá trị.
border-bottom-left-radius
Góc dưới bên trái sẽ được uốn cong. Có thể truyền 1 hoặc 2 giá trị.
border-bottom-right-radius
Góc dưới bên phải sẽ được uốn cong. Có thể truyền 1 hoặc 2 giá trị.
# Những website lấy icon 
    • Fontawasome
    • Adnjs
    • Boxicons.com
    • Ionicons