# 事件的冒泡

事件冒泡指的是，事件的向上传导。当一个后代元素被触发时，其父元素以及祖先元素的相同事件也被触发

在开发中，大部分冒泡都是有用的
- 比如，上一个div跟随鼠标移动
- 我们绑定了document.onmousemove事件，当鼠标在整个网页上移动时，都会跟随
- 但是当页面上还有其他div等元素的时候，如果不冒泡
- 那么即使鼠标启动过去，div也不会跟随

但有时，也只需要仅在子元素上执行，而不需要冒泡到父元素上，通过**事件对象**可以手动取消
```javascript
sonObj.onclick = function(e){
  e = e || window.e;
  e.cancelBubble = true;
}

FatherObj.onclick = function(e){
  e = e || window.e;
  e.cancelBubble = true;
}
```

![Feb-08-2020 14-58-57](https://user-images.githubusercontent.com/26485327/74080896-93db1080-4a83-11ea-89be-fa554e2edc15.gif)


```html
<html>
<head>
    <style>
        body {
            height: 1000px;
            width: 1000px;
        }
        
        #box1 {
            width: 100px;
            height: 100px;
            background-color: red;
            position: absolute;
        }
        
        #box2 {
            width: 200px;
            height: 200px;
            background-color: lightcyan;
        }
    </style>
    <script>
        window.onload = function() {
            var box1 = document.getElementById('box1');
            var box2 = document.getElementById('box2');
            var top = document.body.scrollTop || document.documentElement.scrollTop;
            var left = document.body.scrollLeft || document.documentElement.scrollLeft;

            document.onmousemove = function(e) {
                e = e || window.e;
                box1.style.left = e.pageX + left + 'px';
                box1.style.top = e.pageY + top + 'px';
            };
            box2.onmousemove = function(e) {
                e = e || window.e;
                e.cancelBubble = true;
            };
        };
    </script>
</head>

<body>
    <div id="box1"></div>
    <div id="box2"></div>
</body>
</html>
```
