
# 点住鼠标移动方块，桌面拖动图标
1. div的样式需要开启定位
    - box必须设置position，才可以根据设置的样式位置参数来移动
2. onmousedown，点住鼠标
3. onmousemove，鼠标移动需要在onmousedown事件函数内部执行
    - 跟随鼠标移动时，事件要绑定到document，而不能绑定box1
        - 如果onmousemove事件绑定给box1，当鼠标移出box1的外翻之内，onmousemove事件将无法被触发，也就不能移动box1
4. onmouseup，松开鼠标
    - 首先onmouseup不能绑定给box1，因为box1走到其他元素，如兄弟节点box2元素时，由于冒泡，box1的鼠标事件将失效，因为其他元素上没有绑定任何事件
    - 当松开鼠标时，onmousemove事件需要停止，设置为null
    - 同样鼠标松开后，onmouseup事件自己本身也要设置为null
        - 否则点击document页面的空白地方，松开鼠标一样会触发此事件

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
- 问题：鼠标点中无论box1的哪一点，鼠标都会自动复位到div的默认左上角，体验不好
                  
                  
                  
                  
                  
