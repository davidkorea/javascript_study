
Chapter121 mouse scroll...

# 点住鼠标移动方块，桌面拖动图标

#### 1. div开启定位
- box必须设置position，才可以根据设置的样式位置参数来移动
#### 2. onmousedown，点住鼠标
#### 3. onmousemove，鼠标移动
- 需要在onmousedown事件函数内部执行
- 跟随鼠标移动时，事件要绑定到document，而不能绑定box1
    - 如果onmousemove事件绑定给box1，当鼠标移出box1的外翻之内，onmousemove事件将无法被触发，也就不能移动box1
#### 4. onmouseup，松开鼠标
- 首先onmouseup不能绑定给box1，而要绑定给document
    - 因为box1走到其他元素，如兄弟节点box2元素时，~~由于冒泡~~，**兄弟节点之间没有冒泡，只有父子节点会冒泡**
    - 鼠标移动到box2时，会触发box2的事件，所以box1的鼠标移动事件将失效
- 当松开鼠标时，onmousemove事件需要停止，设置为null
- 同样鼠标松开后，onmouseup事件自己本身也要设置为null
    - 否则点击document页面的空白地方，松开鼠标一样会触发此事件
- **因为onmousemove和onmouseup事件都是在onmousedown事件下面执行，当鼠标不是在onmousedown的状态下时，这两个内层事件都要被取消**

![Feb-08-2020 22-28-50](https://user-images.githubusercontent.com/26485327/74086904-6b263b80-4ac2-11ea-9eb0-f9d230bcd2c2.gif)


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
                  
# 2. 保持鼠标位置不变
因为在box1里面，每次点住鼠标，box1为自动调到鼠标所在位置，导致在移动鼠标之前，box1会跳动，感觉不友好。要解决，需要获取鼠标相对于box1左上定点的距离，并保持该相对距离不变。因此要讲box1的跳动的偏移量找到，在给box1重新加回去
- div的水平偏移量 = 鼠标.clientX - 元素.offsetLeft
- div的垂直偏移量 = 鼠标.clientY - 元素.offsetTop

<img width="350" height="350" src="https://user-images.githubusercontent.com/26485327/74087516-f6560000-4ac7-11ea-9213-9e0986f26f93.jpeg" >


```javascript
var offsetX = e.clientX - box1.offsetLeft;
var offsetY = e.clientY - box1.offsetTop;
```

![Feb-08-2020 23-12-25](https://user-images.githubusercontent.com/26485327/74087560-7ed4a080-4ac8-11ea-8a3f-35c876e5d245.gif)
                  
```javascript
window.onload = function() {
    var box1 = document.getElementById('box1');

    box1.onmousedown = function(e) {           // 这个e和下面函数的e不是同一个
        e = e || window.e;
        var offsetX = e.clientX - box1.offsetLeft;
        var offsetY = e.clientY - box1.offsetTop;

        document.onmousemove = function(e) {
            e = e || window.e;
            var left = e.clientX - offsetX;
            var top = e.clientY - offsetY;
            box1.style.left = left + 'px';
            box1.style.top = top + 'px';
        };
        document.onmouseup = function() {
            document.onmousemove = null;
            document.onmouseup = null;
        };
    }
}
```

# 3. 浏览器自动搜索被拖拽元素

浏览器自动搜索网页中拖拽的文字或图片，因此要取消浏览器这个默认行为。通过return false可以取消，但是不支持IE8

```javascript
元素.onmousedown = function(){
    ...
    return false
}
```

对于IE8，setCapture
```javascript
box1.onmousedown = function(){
    box1.setCapture();         // 捕获下一次鼠标点击事件，强制绑定到box1上，无论点击哪里
     
    document.onmousemove = function(){
        ...
    }
    document.onmouseup = function(){
        。。。
        box1.releaseCapture();  // 当鼠标松开后，定制强制绑定事件
    }
}
```
- 通过强制绑定事件，来把所有鼠标操作都绑定给box1的移动，来避免拖拽搜索

兼容所有浏览器

```javascript
box1.onmousedown = function(){

    if(box1.setCapture){
        box1.setCapture();   
    };
    
    // box1.setCapture && box1.setCapture(); 
          
    document.onmousemove = function(){
        ...
    }
    document.onmouseup = function(){
        。。。
        box1.releaseCapture && box1.releaseCapture();  
    }
    return false                    // firefox,chrome
}
```

- `box1.setCapture && box1.setCapture();`，` box1.releaseCapture && box1.releaseCapture();`
    - 当前面为true，则执行后面语句
    - 前面为false，则直接放弃执行

# 4. 设置2个box都可以移动


![Feb-09-2020 12-53-48](https://user-images.githubusercontent.com/26485327/74096558-83866c80-4b3b-11ea-8bfb-8121e345f79f.gif)

```javascript
window.onload = function() {
    function dragBox(boxId) {
        var box = document.getElementById(boxId);
        box.onmousedown = function(e) {
            e = e || window.e
            var offsetLeft = e.clientX - box.offsetLeft;
            var offsetTop = e.clientY - box.offsetTop;

            box.setCapture && box.setCapture();

            document.onmousemove = function(e) {
                e = e || window.e
                box.style.left = e.clientX - offsetLeft + 'px';
                box.style.top = e.clientY - offsetTop + 'px';
            }
            document.onmouseup = function() {
                document.onmousemove = null;
                document.onmouseup = null;
                box.releaseCapture && box.releaseCapture();
            }
            return false
        }
    }

    dragBox('box1');
    dragBox('box2');
}
```


