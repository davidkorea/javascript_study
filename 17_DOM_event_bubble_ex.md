# 事件的冒泡，委派，传播

## 1. 事件的冒泡

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


## 2. 事件的委派
将事件统一绑定到一组元素的共同祖先，这样后代元素触发时，会自动冒泡到祖先元素
- 事件委派利用了冒泡
- 通过委派可以减少事件绑定的次数，提供性能

#### 练习：点击链接显示内容，点击按钮添加新链接
```html
<html>
<head>
    <script>
        window.onload = function() {
            var btn = document.getElementById('btn');
            var allA = document.getElementsByTagName('a');

            // click link to show msg
            for (i = 0; i < allA.length; i++) {
                allA[i].onclick = function() {
                    alert('hi');
                }
            };

            // click to add new link
            var u1 = document.getElementById('u1');
            btn.onclick = function() {
                var li = document.createElement('li');
                li.innerHTML = "<a href='javascript:;'>new link</a>";
                u1.appendChild(li);
            };
        };
    </script>
</head>

<body>
    <button id="btn">add</button>
    <ul id="u1">
        <li><a href="javascript:;">link1</a></li>
        <li><a href="javascript:;">link2</a></li>
        <li><a href="javascript:;">link3</a></li>
    </ul>
</body>
</html>
```
- 问题1：原来就有的超链接，可以有单击响应事件，而新添加的链接，没有点击事件，需要重新绑定
  - 希望只绑定依次事件，即可应用到所有原有和新添加的元素
  - 可以考虑**将事件绑定到所有新旧元素共同的祖先**，事件委派！！！
- 问题2：事件委派很好，但是容易造成，点击所有父元素区域都执行操作，而不是指定的子元素
  - 通过浏览器传给事件函数的实参：**事件对象**，来获取当前点击的对象`event.target`，如果是对应的子元素对象，则执行，否在不执行
  
  
![Feb-08-2020 16-08-46](https://user-images.githubusercontent.com/26485327/74081751-7448e580-4a8d-11ea-9222-2526ea4c8bbe.gif)
  

```html
<html>
<head>
    <script>
        window.onload = function() {
            var btn = document.getElementById('btn');
            var allA = document.getElementsByTagName('a');
            var u1 = document.getElementById('u1');

            // click link to show msg
            // for (i = 0; i < allA.length; i++) {
            //     allA[i].onclick = function() {
            //         alert('hi');
            //     }
            // };
            u1.onclick = function(e) {
                e = e || window.e;
                if (e.target.id == "link") {
                    alert('hi');
                }
            };

            // click to add new link
            btn.onclick = function() {
                var li = document.createElement('li');
                li.innerHTML = "<a href='javascript:;' id='link'>new link</a>";
                u1.appendChild(li);
            };
        };
    </script>
</head>

<body>
    <button id="btn">add</button>
    <ul id="u1">
        <li><a href="javascript:;" id="link">link1</a></li>
        <li><a href="javascript:;" id="link">link2</a></li>
        <li><a href="javascript:;" id="link">link3</a></li>
    </ul>
</body>
</html>
```
  
## 3. 事件的传播，捕获
当子元素，父元素，祖先元素等多元素嵌套时，会出现冒泡，但是冒泡的先后顺序，也叫做传播顺序
- 微软，由内向外，由子元素相外层祖先元素传播。即先触发子元素事件
- 网景，由外向内，先出发祖先元素事件，依次向内。也叫做事件的捕获

W3C决定，综合两个公司方案，将事件传播分成了三个阶段。
- 当点击一个元素时
  1. 捕获阶段，有外向内，但是默认此时不会触发事件
  2. 目标阶段，从外向内捕获到所点击元素，但是不会触发事件
  3. 冒泡阶段，开始在目标元素上执行事件，并且由内向外，分别依次执行外层元素上的事件
  
  
- 如果希望在捕获阶段就触发事件，可讲addEventLisener()的第三个参数设置为true
  - 此时事件执行顺序为先执行外层祖先元素事件，直观感受上不舒服，顺序有问题，因此很少使用
  - 一般不会在捕获阶段执行事件



