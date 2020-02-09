# 浏览器对象模型

BOM提供了一组对象来操作浏览器
- window
  - 整个浏览器窗口，也是网页中的全局对象
- navigator
  - 当前浏览器的信息，识别不同类型浏览器
- location
  - 浏览器当前地址栏信息，或者操作浏览器跳转页面
- history
  - 浏览器历史记录，由于隐私原因，不能获取到具体的历史记录，只能操作浏览器向前向后翻页
  - 只在档次访问时有效
- screen
  - 用户的屏幕（显示器）信息
  - 更多用在移动端
  
  
BOM对象在浏览器中
- 作为window的属性保存，可以window.navigator，window.location
- 也作为全局变量，可以直接调用navigator，location

# 1. navigator

![6550452B-DC67-47EA-9376-363C3B781137](https://user-images.githubusercontent.com/26485327/74097945-1976c300-4b4d-11ea-9b15-1b1c9cfb937f.jpeg)

- 由于历史原因，navigator的大部分属性，不能用来有效确认浏览器信息
- 一般只会使用userAgent，**用户代理等价于浏览器**
  - 不同浏览器有不同userAgent
  - `Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.130 Safari/537.36`
  - `Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.5 Safari/605.1.15`
  ```javascript
  var userAgent = navigator.userAgent;
  
  if (/chrome/i.test(userAgent)) {          // i 忽略大小写
      alert('chrome');
  } else if (/safari/i.test(userAgent)) {
      alert('safari');
  } else {
      alert('???');
  }
  ```
- 如果userAgent不能判断浏览器信息，如IE11，则找到IE11独有的一些对象，如果有就是IE11
  ```javascript
    if (window.ActiveXObject) {       // IE 8,9,10 ok
        alert('IE');
    }
  ```
  - 虽然IE11有这个属性，但是转换成boolean时，时false，微软做了手脚
  ```javascript
  if ('ActiveXObject' in window) {    // IE 11
      alert('IE');
  }
  ```

# 2. history

![F1B25958-6C19-4325-8E6B-BB01C31D5C77](https://user-images.githubusercontent.com/26485327/74102424-5effb400-4b7e-11ea-9bf0-128c926c60e1.jpeg)


操作浏览器向前向后翻页，浏览器关闭后，历史记录消失
属性
- length，访问页面的个数
方法
- back，同浏览器后退按钮
- forward，同浏览器前进按钮
- go，跳转到指定界面，需要整数参数
  - go(1)，向前1个页面
  - go(-1)，向后1个页面
  
# 3. location
地址栏
- console.log(location)，当前页面的地址
- `location = www.a.com`，修改location的值，可以实现页面跳转，并生成响应的历史记录history  

![74A3B1CF-3B03-47FE-99A1-9E50D530063E](https://user-images.githubusercontent.com/26485327/74102428-63c46800-4b7e-11ea-93ec-4b4c902705a8.jpeg)

属性，如图

方法
- assign，和直接给location赋值的效果一样
- reload，重新加载当前页面，和浏览器刷新按钮一样
  - `reload(true)`，强制清空缓存刷新界面，清楚一个输入框里面的信息等
- replace，也可以跳转页面，但是不能后退回去，不生成历史记录
  
# 4. screen
![0012931E-D146-4258-A011-5893658A4478](https://user-images.githubusercontent.com/26485327/74102430-658e2b80-4b7e-11ea-86b2-19974e1861af.jpeg)

# 5. window

## 5.1 定时调用 setInterval

每间隔一段时间，发生一次

- setInterval(function(){}, ms)，将一个函数（回调函数），每隔一段时间执行依次
  - 返回值，是个数字，作为定时器的唯一标识，用于关闭定时器
  - clearInterval()关闭定时器，可以接收任意参数，如undefined，null都可以
    - 如果参数有效，则停止定时器，参数无效则无动作。！！！很关键，因为一般会在一个定时器开启时，先停掉前面所有的定时器
      - 函数第一次运行，前面没有定时器，但是也要执行停止计时器，因为无效参数不报错，此处可以放心使用
    
![E5708F2D-484B-48FF-A0BB-7AEBB6BFD499](https://user-images.githubusercontent.com/26485327/74102447-7dfe4600-4b7e-11ea-8b53-53429a85c9e4.jpeg)  
  
```html
<html>
<head>
    <script>
        window.onload = function() {
            var h1 = document.getElementById('h1');

            var num = 1;
            var timer1 = setInterval(() => {    // 每隔1000ms执行一遍这里的函数
                h1.innerHTML = num++;
                if (num == 11) {
                    clearInterval(timer1);      // 关闭定时器
                }
            }, 1000);
        };
    </script>
</head>

<body>
    <h1 id="h1"></h1>
</body>
</html>
```
### 练习：图片滚动

```html
<html>
<head>
    <style>
        div {
            width: 500px;
            text-align: center;
            padding-top: 10px;
        }
    </style>
    <script>
        window.onload = function() {
            var btn1 = document.getElementById('btn1');
            var btn2 = document.getElementById('btn2');

            var timer1; // 全局定义完成，在函数内部赋值使用！！！

            btn1.onclick = function() {
                var img = document.getElementsByTagName('img')[0];
                var imgList = ['1.png', '2.png', '3.png', '4.png'];
                var idx = 0;
                timer1 = setInterval(() => {
                    idx++;
                    console.log(idx);

                    img.src = imgList[idx];
                    if (idx > imgList.length - 2) {
                        idx = -1;
                    }
                }, 1000);
            };

            btn2.onclick = function() {
                clearInterval(timer1);
                console.log('pause');
            }
        };
    </script>
</head>

<body>
    <img src="1.png" width="500" height="300">
    <div>
        <button id="btn1">start</button>
        <button id="btn2">pause</button>
    </div>
</body>
</html>
```
- 全局作用域定义变量，在一个事件函数中为其赋值，可以在另一个函数中调用改变量
  - 如果直接创建事件函数内，则无法在其他函数中调用
- 问题：可以无线点击开始按钮，导致每次都会重新开始一个滚动时间，而pause只能暂停左后一个，之前的都不能取消
  - 解决：在onclick事件出发后，首先停止一下计数器clearInterval，以用于万一再次之前已经有一次滚动事件触发


![Feb-09-2020 20-51-08](https://user-images.githubusercontent.com/26485327/74102375-f6183c00-4b7d-11ea-92b9-2a2e61ab3821.gif)


```javascript
window.onload = function() {
    var btn1 = document.getElementById('btn1');
    var btn2 = document.getElementById('btn2');

    var timer1; // 全局定义完成，在哦函数内部赋值使用！！！

    btn1.onclick = function() {
        clearInterval(timer1);    // 开始计时器之前先取消之前的，如果之前已经开了一个定时器

        var img = document.getElementsByTagName('img')[0];
        var imgList = ['1.png', '2.png', '3.png', '4.png'];
        var idx = 0;
        timer1 = setInterval(() => {
            idx++;
            console.log(idx);

            img.src = imgList[idx];
            if (idx > imgList.length - 2) {
                idx = -1;
            }
        }, 1000);
    };

    btn2.onclick = function() {
        clearInterval(timer1);
        console.log('pause');
    }
};
```
- 开启计时器之前，关闭当前元素上的其他定时器
  
  
## 5.2 延时调用 setTimeout

函数不马上哈执行，一段时间后在执行，只会执行一次，而定时调用会持续执行。cleartimeout关闭延时调用



  
  
  
  
  
  
  
