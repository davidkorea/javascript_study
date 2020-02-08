# 事件对象

事件的响应函数被触发时，浏览器每次都会将**事件对象**当做实参，传入响应发函数
- 无论是onscroll，onclick还是onmousemove，浏览器传给响应函数的实参是一样的，叫做MouseEvent
- 该事件对象封装了当前对象的一切信息，鼠标滚轮，按下的键盘按键等等
- 事件响应函数投过一个形参就可以接收浏览器传给的这个实参
- clientX，clientY为鼠标位置


<img width="667" src="https://user-images.githubusercontent.com/26485327/74079732-3d1b0a00-4a76-11ea-9de1-b56603a3d075.png">

```html
<html>
<head>
    <style>
        #mouseDiv {
            width: 300px;
            height: 100px;
            border: 2px solid;
            margin: 10;
        }
        
        #msgDiv {
            width: 300px;
            height: 20px;
            border: 2px solid;
            margin: 10;
            text-align: center;
        }
    </style>
    <script>
        window.onload = function() {
            var mouseDiv = document.getElementById('mouseDiv');
            var msgDiv = document.getElementById('msgDiv');
            mouseDiv.onmousemove = function(e) {
                msgDiv.innerText = "X = " + e.clientX + ", Y = " + e.clientY;
            }
        };
    </script>
</head>

<body>
    <div id="mouseDiv"></div>
    <div id="msgDiv"></div>
</body>
</html>
```

- IE8中，浏览器不会传递该**事件对象**实参给响应函数，而是将事件对象最为window的属性保存
    - 响应函数中，通过调用window.event即可使用
    
- 兼容多浏览器

```javascript
mouseDiv.onmousemove = function(e) {
    if(!e){
        e = window.e;
    }
    msgDiv.innerText = "X = " + e.clientX + ", Y = " + e.clientY;
}
```








