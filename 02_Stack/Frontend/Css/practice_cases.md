# Tạo icon youtube
```html
<body>
    <div class="wrapper">
        <div class="hexagon"></div>
        <div class="hexInner1"></div>
        <div class="hexInner2"></div>
        <div class="triangle"></div>
    </div>
</body>
```
```css
*{
    padding: 0;
    margin: 0;
}
body{
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}
.wrapper{
    position: relative;
    width: 400px;
    height: 400px;
    display: flex;
    justify-content: center;
    align-items: center;
}
. hexagon{
    position: absolute;
    width: 10em;
    height: 17.32em;
    background-color: rgb(255, 0, 0);
    border-radius: 1em / 0.5em;
    transform: rotate(90deg);
}


.hexagon::before, .hexagon::after{
    content: "";
    position: absolute;
    width: inherit;
    height: inherit;
    background-color: inherit;
    border-radius: inherit;
}
.hexagon::before{
    transform: rotate(60deg);
}
.hexagon::after{
    transform: rotate(120deg);
}

.hexInner1{
    position: absolute;
    width: 10em;
    height: 17.32em;
    background-color: #fff;
    border-radius: 1em / 0.5em;
    transform: rotate(90deg) scale(0.65);
}
hexInner1::before, .hexInner1::after{
    content: "";
    position: absolute;
    width: inherit;
    height: inherit;
    background-color: inherit;
    border-radius: inherit;
}

.hexInner1::before{
    transform: rotate(60deg);
}
.hexInner1::after{
    transform: rotate(120deg);
}
.hexInner2{
    position: absolute;
    width: 10em;
    height: 17.32em;
    background-color: rgb(255, 0, 0);
    border-radius: 1em / 0.5em;
    transform: rotate(90deg) scale(0.59);
}
.hexInner2::before, .hexInner2::after{
    content: "";
    position: absolute;
    width: inherit;
    height: inherit;
    background-color: inherit;
    border-radius: inherit;
}
.hexInner2::before{
    transform: rotate(60deg);
}
.hexInner2::after{
    transform: rotate(120deg);
}
.triangle{
    position: absolute;
    border-top: 50px solid transparent;
    border-left: 80px solid #fff;
    border-bottom: 40px solid transparent;
    left: 172px;
}
```