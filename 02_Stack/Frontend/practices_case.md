# Tạo trường đăng nhập (Username) bằng html + css
**Ex1**
```html
 <div class="input-box">
  <input type="text" required>
  <label for="">Username</label>
 </div>
```
```css
*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: sans-serif;
}
body{
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background-color: #1d2b3e;
}
.input-box{
    position: relative;
    width: 280px;
    margin: 20px 0;
}
.input-box label{
    position: absolute;
    top: 50%;
    left: 5px;
    transform: translateY(-50%);
    font-size: 16px;
    color: rgba(255,255,255, 0.3);
    padding: 0 5px;
    pointer-events: none;
}
.input-box input{
    width: 100%;
    padding: 10px;
    background: transparent;
    border: 1.8px solid rgba(255,255,255,0.3);
    outline: none;
    border-radius: 5px;
    color: #fff;
    transition: 0.5s;
}
.input-box input:focus~label,
.input-box input:valid~label{
    top: 0;
    left: 10px;
    font-size: 11px;
    background: #1d2b3e;
    transition: 0.5s;
}
```
**Ex2**
```html
 <div id="UserName">
  <input type="text">
  <label for="">Username</label>
  <i class="fa-solid fa-user"></i>
 </div>
```
```css
*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: sans-serif;
}
body{
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}
#UserName{
    position: relative;
    border: 2px solid #000;
    border-radius: 5px;
}
#UserName input{
    padding: 10px 10px;
    border: none;
    width: 260px;
    outline: none;
}
#UserName label{
    position: absolute;
    top: 50%;
    left: 5px;
    transform: translateY(-50%);
    pointer-events: none;
}
#UserName input:focus~label{
    top: 0px;
    left: 10px;
    font-size: 15px;
    border: none;
    background: #fff;
    padding: 0px 8px;
    transition: .5s;
}
.fa-user{
    margin: 0 7px;
}
```