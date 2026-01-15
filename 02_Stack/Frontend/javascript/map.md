# map()
```bash
- Chỉnh sửa, thay đổi trong mảng.
- Để tạo ra một mảng mới bằng cách áp dụng một hàm lên từng phần tử của mảng bao đầu. Cho phép biến đổi các phần tử một cách dễ dàng và trả về một mảng mới chứa kết quả được biến đổi
```
```js
var a = [1,2,3,4];
var c  = a.map(function (b){
    return b+2;
})
console.log(c); # [3,4,5,6]
```