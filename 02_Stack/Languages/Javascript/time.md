- [setTimeout() \& setInterval()](#settimeout--setinterval)
- [clearInterval()](#clearinterval)
  - [đồng hồ bấm giờ](#đồng-hồ-bấm-giờ)
---
# setTimeout() & setInterval()
```bash
- Thiết lập một khoảng thời gian nào đó sẽ thực hiện một nhiệm vụ nào đó và nó chỉ thực hiện đúng một lần. 
- setTimeout    : chỉ được sử dụng với function.
- setInterval   : số lần thực hiện lã mãi mãi
```
**Syn**
```bash
setTimeout(function, time);

- function: Là nội dung cần thực hiện, đây là một hàm.
- time: Là khoảng thời gian bao nhiêu (tính bằng mili giây) thì function đó sẽ thực hiện.
```
# clearInterval() 
```bash
Xóa đi một nhiệm vụ nào đó của setTimeout.
```
**Ex**
```html
<button>Dừng</button>
<p></p>
```
```js
let i = 0;
let text = document.getElementsByTagName("p");
function time() {
    text[0].innerHTML = i++;
}
function main() {
    let res = setInterval(time, 1000);
    let stop = document.getElementsByTagName("button");
    stop[0].onclick = function (){
        clearInterval(res)
    }
}
main();
```
## đồng hồ bấm giờ
```js
let second = document.getElementById("seconds");
let minute = document.getElementById("minutes");
let count = 56;
let mis = 0;
function Minute(){
    if(count == "60"){
        count = 0;
        mis += 1;
        minute.innerHTML = mis;
    }
}
function TimeMath(){
    count++;
    if(count < 10){
        count = "0" + count;
    }
    second.innerHTML = count;
    Minute();
}
function main(){
    let res = setInterval(TimeMath, 1000)
    let but = document.getElementById("stop");
    but.onclick = function (){
        clearInterval(res);
    }
}
main()
```