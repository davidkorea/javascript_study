
# 点住鼠标移动方块，桌面拖动图标

- box必须设置position，才可以根据设置的样式位置参数来移动

```html
<html>
<head>
    <style>
        #box1 {
            height: 100px;
            width: 100px;
            background-color: red;
            position: absolute;       // 必须设置position！！
        }
        
        #box2 {
            height: 100px;
            width: 100px;
            left: 200px;
            top: 200px;
            background-color: lightcyan;
            position: absolute;
        }
    </style>
    <script>
        // 鼠标点住box1时，跟随鼠标移动，鼠标松开停止移动
        window.onload = function() {
            var box1 = document.getElementById('box1');
            var box2 = document.getElementById('box2');

            box1.onmousedown = function() {
                document.onmousemove = function(e) {
                    e = e || window.e;
                    var left = e.clientX;
                    var top = e.clientY;
                    box1.style.left = left + 'px';
                    box1.style.top = top + 'px';
                };
                document.onmouseup = function() {
                    document.onmousemove = null;
                    document.onmouseup = null;
                };
            }
        }
    </script>
</head>

<body>
    <div id="box1"></div>
    <div id="box2"></div>
</body>
</html>
```
