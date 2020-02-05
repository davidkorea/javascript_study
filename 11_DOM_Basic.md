

# DOM, Document Object Model, 文档对象模型

前面说到的都是自定义对象以及ES自建对象，DOM是浏览器提供的**宿主对象**

# 1. Basics

### 1.DOM
js可以通过DOM文档对象模型来操作html页面
- 文档： html网页
- 对象： 网页的每个部分都转换成了对象，包括标签，文本等
- 模型： 表示对象与对象之间的关系，比如一个超链接标签是属于 html.boday.div.a，如下图
<img width="488" src="https://user-images.githubusercontent.com/26485327/73812566-3000df80-4818-11ea-8107-8873991f20a4.png">



### 2. 节点 Node
- 构成网页的最基本的部分，网页中的每一个部分都可以称作节点。就如同网络中的每个pc，每个路由器等网络设备都可以称作节点
- btml标签，属性，文本，注释，整个文档本身，都是一个节点，但是分别属于不同的节点类型
  - 元素节点 Element
  - 属性节点 Attr
  - 本文节点 Text
  - 文档节点 Document
<img width="575" src="https://user-images.githubusercontent.com/26485327/73812295-43f81180-4817-11ea-9b97-77731820ae05.png">

- 节点的属性，**节点的类型不同，所具有的属性和方法也不同**
<img width="470" src="https://user-images.githubusercontent.com/26485327/73812390-93d6d880-4817-11ea-8942-c257ae687735.png">

```javascript
<button id='btn'>Click</button>

<script>
    console.log(document.getElementById('btn'));
    var btn = document.getElementById('btn');
    btn.innerHTML = 'hi';
</script>
```
- 浏览器提供文档节点document，文档节点对象就是window的属性

### 3. 事件 Event

- 事件就是用户和浏览器的交互行为，比如点击按钮，鼠标移动，调整浏览器网页大小，关闭一个网页等
- 重要的是如何处理事件，在事件对应的属性中，添加js代码。当事件触发时，将执行js代码
- 为事件绑定响应函数
```javascript
<button id='btn'>Click</button>
<script>
    var btn = document.getElementById('btn');
    btn.onclick = function() {
        alert('hi')
    };
</script>
```

### 4. 浏览器加载页面顺序
```javascript
<html>
<head>
    <script>
        var btn = document.getElementById('btn');   // 由于下面还没加载，此时无法获得该btn按钮
        btn.onclick = function() {
            console.log('hi');
        };
    </script>
</head>

<body>
    <button id="btn">Click</button>
</body>
</html>
```
<img width="655" alt="截屏2020-02-05下午2 01 28" src="https://user-images.githubusercontent.com/26485327/73815154-05b32000-4820-11ea-821e-7165444de533.png">

- 浏览器自上向下加载页面，加载一行运行一行
- js代码在上面加载运行时，下面的html还没有加载，**页面没有加载完成则DOM对象也没有加载**，会导致报错
- 那么需要上方的代码，等待整个html页面加载完成后在运行。而**等待页面加载完成onload，也是一个事件！**
  - 为window绑定onload事件

```javascript
<head>
    <script>
        window, onload = function() {
            var btn = document.getElementById('btn');
            btn.onclick = function() {
                console.log('hi');
            };
        };
    </script>
</head>

<body>
    <button id="btn">Click</button>
</body>
```
<img width="506" alt="截屏2020-02-05下午2 09 52" src="https://user-images.githubusercontent.com/26485327/73815518-3051a880-4821-11ea-9035-fef5e5bdfe6a.png">


# 2. 元素节点对象
- document.getElementById('btn')，通过元素id，获得一个元素
- document.getElementsByTagName('div')，通过元素标签名，获得一组元素，div，span
  - 返回一个数组，可以使用length查看数组长度
  - 可以通过innerHTML获取标签内部的内容
- document.getElementsByName，通过元素名称，获得一组元素，表单和按钮一般由名称属性
  - 返回一个数组
  - 对于自结束标签`<input name='gender' type='text' value='male'/>`，不能使用innerHTML，获取不到内容
  - 可以读取标签的属性，直接.属性 `.name`，`.value` 即可，唯独特殊的是class不能这样来读取
  - `<input class='hello' name='gender' type='radio' value='male'/>`，需要通过`.className`来获取标签的class属性，因为class是js的关键字，不能直接使用

#### 练习：切换图片
```javascript
<html>

<head>
    <style>
        *. {
            margin: 0;
            padding: 0;
        }
        
        #outer {
            width: 500px;
            margin: 50px auto;
            padding: 10px;
            background-color: bisque;
            text-align: center;
        }
        
        #inner {
            width: 500px;
        }
    </style>

    <script>
        window.onload = function() {

            var imglist = ['1.png', '2.png', '3.png', '4.png'];
            var imgtag = document.getElementsByTagName('img');
            var prevBtn = document.getElementById('prev');
            var nextBtn = document.getElementById('next');
            var imgidx = imglist.indexOf(imgtag[0].src.split('/')[6]);
            var info = document.getElementById('info');
            info.innerHTML = (imgidx + 1) + ' of ' + imglist.length + ' pics.';

            prevBtn.onclick = function() {
                if (imgidx > 0) {
                    imgidx--;
                    imgtag[0].src = imglist[imgidx];
                    info.innerHTML = (imgidx + 1) + ' of ' + imglist.length + ' pics.';
                } else {
                    imgtag[0].src = '1.png';
                }
            };

            nextBtn.onclick = function() {
                if (imgidx < imglist.length - 1) {
                    imgidx++;
                    imgtag[0].src = imglist[imgidx];
                    info.innerHTML = (imgidx + 1) + ' of ' + imglist.length + ' pics.';

                } else {
                    imgtag[0].src = imglist[imglist.length - 1];
                }
            }
        }
    </script>
</head>

<body>
    <div id="outer">
        <p id="info"></p>
        <img src="2.png" width="500px" height="300px">
        <button id="prev">prev</button>
        <button id="next">next</button>
    </div>
</body>

</html>
```

优化代码
```javascript
window.onload = function() {
    var imglist = ['1.png', '2.png', '3.png', '4.png'];
    var imgtag = document.getElementsByTagName('img')[0];
    var prevBtn = document.getElementById('prev');
    var nextBtn = document.getElementById('next');
    var imgidx = imglist.indexOf(imgtag.src.split('/')[6]);   // ["file:", "", "", "Users", "yong", "Desktop", "2.png"]
    var info = document.getElementById('info');
    info.innerHTML = (imgidx + 1) + ' of ' + imglist.length + ' pics.';

    prevBtn.onclick = function() {
        imgidx--;
        if (imgidx < 0) {
            imgidx = 0;
        }
        imgtag.src = imglist[imgidx];
        info.innerHTML = (imgidx + 1) + ' of ' + imglist.length + ' pics.';
    };

    nextBtn.onclick = function() {
        imgidx++;
        if (imgidx > imglist.length - 1) {
            imgidx = imglist.length - 1
        }
        imgtag.src = imglist[imgidx];
        info.innerHTML = (imgidx + 1) + ' of ' + imglist.length + ' pics.';
    }
}
```

![](https://user-images.githubusercontent.com/26485327/73828071-9cd9a100-483b-11ea-8aa6-4e8d9a6beb89.gif)


# 3. 元素节点的子节点

上面元素节点对象都是document.开始的，元素的子节点实在当前元素对象的基础上，在实现方法和属性

### 1. 方法
- `元素节点.getElementsByTagName()`
```javascript
var outer = document.getElementById('outer');
console.log(outer.getElementsByTagName('img'));   //   var outer = document.getElementById('outer');
```
### 2. 属性
- `元素节点.childNodes`，当前节点的所有子节点
```javascript
var outer = document.getElementById('outer');
console.log((outer.childNodes));
```
```
// NodeList(9) [text, p#info, text, img, text, button#prev, text, button#next, text]
```

- `元素节点.firstChild`，当前节点的第一个子节点
```javascript
var outer = document.getElementById('outer');
console.log((outer.firstChild));      // #text
```


- `元素节点.lastChile`，当前节点的最后一个节点
```javascript
var outer = document.getElementById('outer');
console.log((outer.lastChild));       // #text
```   










