- [background-color](#background-color)
---
CSS Colors
Color name
Sử dụng tên màu bằng tiếng anh để gán giá trị màu cho phần tử.
RGB
Sử dụng hệ màu phối của red – green – blue để gán giá trị màu cho phần tử, Giá trị cao nhất là 255, thấp nhất là 0.
RGBA
Giống với rgb những thêm độ trong suốt (alpha) ở phần cuối.
HEX
Sử dụng giá trị thập lục phân để gán giá trị cho phần tử. thêm # ở phần đầu.
Có 6 giá trị cứ 2 cặp là 1 nhóm của rgb.
HSL
Sử dụng bảng màu theo vòng tròn màu sắc.

Cú pháp:
hsl (hue, saturation, lightness);
    • Hue: Là độ của màu trong vòng tròn, có giá trị từ 0 đến 360
        ◦ 0 là màu đỏ
        ◦ 120 là màu xanh lá cây
        ◦ 240 là màu xanh da trời
    • Saturation: là cường độ màu, có giá trị từ 0% đến 100%
    • Lightness: là độ sáng của màu, có giá trị từ 0% đến 100%
HSLA
Cách sử dụng giống với HSL nhưng thêm một thành phần alpha vào cuối định dạng độ trong suốt cho màu sắc.
Cú pháp:
hsla(hue, saturation, lightness, alpha)
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="Tester.css">
</head>
<body>
  <div></div>
</body>
</html>
div{
    height: 20px;
    background-color: hsla(0, 100%, 50%, 0.5);
}


HSV (Hue, Saturation, Value)
Là hệ màu không có kênh sáng tối như grayscale, mà nó phân tách rõ về màu sắc


# background-color 
```bash
Để thiết lập màu sắc cho nền của phần tử.
```
**Syn**
```bash
Background-color: CSS colors | transparent
- Transparent: để thiết lập độ trong suốt cho nền
```