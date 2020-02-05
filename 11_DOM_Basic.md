

# DOM, Document Object Model, 文档对象模型

前面说到的都是自定义对象以及ES自建对象，DOM是浏览器提供的**宿主对象**

### 1. **DOM，js可以通过DOM文档对象模型来操作html页面**
- 文档： html网页
- 对象： 网页的每个部分都转换成了对象，包括标签，文本等
- 模型： 表示对象与对象之间的关系，比如一个超链接标签是属于 html.boday.div.a，如下图
<img width="488" src="https://user-images.githubusercontent.com/26485327/73812566-3000df80-4818-11ea-8107-8873991f20a4.png">



###2. **节点Node**
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











