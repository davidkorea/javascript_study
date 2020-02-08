# 事件对象

事件的响应函数被触发时，浏览器每次都会将**事件对象**当做实参，传入响应发函数
- 无论是onscroll，onclick还是onmousemove，浏览器传给响应函数的实参是一样的，叫做MouseEvent
- 该事件对象封装了当前对象的一切信息，鼠标滚轮，按下的键盘按键等等
- 事件响应函数投过一个形参就可以接收浏览器传给的这个实参
- clientX，clientY 为可视浏览器窗口内的鼠标位置
- pageX，pageY 为鼠标相对也整个网页page的为止，但是IE8不支持


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
```javascript
e = e || window.e
```


# 练习：div跟随鼠标移动

![Feb-08-2020 14-39-00](https://user-images.githubusercontent.com/26485327/74080615-ccc5b600-4a80-11ea-9c5a-a73434903c4a.gif)


```html
<html>
<head>
    <style>
    #box1 {
            width: 100px;
            height: 100px;
            background-color: red;
        }
    }
    </style>
    <script>
        window.onload = function() {
            var box1 = document.getElementById('box1');
            document.onmousemove = function(e) {
                e = e || window.e;
                box1.style.left = e.clientX + 'px';
                box1.style.top = e.clientY + 'px';
            }
        };
    </script>
</head>

<body>
    <div id="box1"></div>
</body>
</html>
```
- 由于鼠标坐标只有数值，没有单位，在赋值给div的style时，需要手动添加单位px
- 由于设置style偏移量，元素需要开启定位position，否则虽然有样式，但是元素不会动。**给谁设置样式偏移量，就要给谁开启定位**

```html
<style>
    body {
        height: 1000px;
    }

    #box1 {
        width: 100px;
        height: 100px;
        background-color: red;
        position: absolute;
    }
</style>
<script>
    window.onload = function() {
        var box1 = document.getElementById('box1');
        document.onmousemove = function(e) {
            e = e || window.e;
            box1.style.left = e.clientX + 'px';
            box1.style.top = e.clientY + 'px';
        }
    };
</script>
```
- 当页面body高度超过浏览器可视界面后，将出现滚动条。滚动到页面最后时，鼠标和box无法重合，box无法移动到页面最下端
    - 可以看出，差出来的举例就是滚动条滚动的距离scrollTop
- 原因
    - 鼠标的位置，始终是相对于浏览器课件窗口的位置
    - div的位置，是相当于整个body页面
        - sclientX，clientY，鼠标相对于浏览器可见窗口的位置，此处不能使用
        - pageX，pageY，鼠标相对于整个页面的坐标，但是不支持IE8

- 为了兼容所有浏览器，手动改进添加缺少的scrollTop偏移量以及scrollLeft偏移量
    - chrome & IE 滚动条属于body 
    - firefox 滚动条属于body的父元素html

```javascript
var box1 = document.getElementById('box1');
var top = document.body.scrollTop || document.documentElement.scrollTop;
var left = document.body.scrollLeft || document.documentElement.scrollLeft;

document.onmousemove = function(e) {
    e = e || window.e;
    box1.style.left = e.pageX + left + 'px';
    box1.style.top = e.pageY + top + 'px';
}
```





