
事件函数的默认行为可以在函数最后return false来取消
- input 取消输入
- a 取消自动跳转


# 键盘事件

键盘事件一般绑定给可以获取焦点（光标）的对象，或者是document，而不是div

- onkeydown
  - 如果一直按住一个键不松手，会一直连续不断的触发该事件
  - 第一次会稍微卡一下，后面会连续不断触发，就想在输入框连续输入多个同样的字母，防止误操作

- onkeyup
  - 不会连续触发
  
- 按下了哪个键？浏览器传给的事件对象
  - `event.keyCode`，返回按键的unicode
    - 当不知道某个按键的code时，console.log看一下
  - 按下功能键，alt，shift，ctrl，`event.altKey`，`event.ctrlKey`，`event.shifyKEy`
  - 限制输入数字
  ```javascript
  window.onload = function() {
      var ipt = document.getElementsByTagName('input')[0];
      ipt.onkeydown = function(e) {
          if (e.keyCode >= 48 && e.keyCode <= 57) {
              return false
          }
      }
  }
  ```

### 练习：上下左右按键控制移动方向
- console.log查一下四个方向键的keyCode
  - left 37
  - up 38
  - right 39
  - down 40
  
```html
<html>
<head>
    <style>
        #box1 {
            height: 100px;
            width: 100px;
            background-color: red;
            position: absolute;
        }
    </style>
    <script>
        window.onload = function() {
            var box1 = document.getElementById('box1');

            document.onkeydown = function(e) {
                if (e.keyCode == 37) {
                    box1.style.left = box1.offsetLeft - 10 + 'px';
                } else if (e.keyCode == 38) {
                    box1.style.top = box1.offsetTop - 10 + 'px';
                } else if (e.keyCode == 39) {
                    box1.style.left = box1.offsetLeft + 10 + 'px';
                } else {
                    box1.style.top = box1.offsetTop + 10 + 'px';
                }
            }
        }
    </script>
</head>

<body>
    <div id="box1"></div>
</body>
</html>
```

#### 增加功能：按住shift，移动加速

![Feb-09-2020 14-43-10](https://user-images.githubusercontent.com/26485327/74097717-8c326f00-4b4a-11ea-9bef-82adbc564d71.gif)


```javascript
window.onload = function() {
    var box1 = document.getElementById('box1');

    document.onkeydown = function(e) {
        if (e.shiftKey) {
            step = 100;
        } else {
            step = 10;
        }
        switch (e.keyCode) {
            case 37:
                box1.style.left = box1.offsetLeft - step + 'px';
                break;
            case 38:
                box1.style.top = box1.offsetTop - step + 'px';
                break;
            case 39:
                box1.style.left = box1.offsetLeft + step + 'px';
                break;
            case 40:
                box1.style.top = box1.offsetTop + step + 'px';
                break;
        }
    }
}
```
#### 解决起步卡顿

![Feb-09-2020 21-18-09](https://user-images.githubusercontent.com/26485327/74102771-b7848080-4b81-11ea-94a0-8166efc5f52e.gif)

```javascript
window.onload = function() {
    var box1 = document.getElementById('box1');

    var step = 5;
    var dir = 0;

    setInterval(function() {

        switch (dir) {
            case 37:
                box1.style.left = box1.offsetLeft - step + 'px';
                break;
            case 38:
                box1.style.top = box1.offsetTop - step + 'px';
                break;
            case 39:
                box1.style.left = box1.offsetLeft + step + 'px';
                break;
            case 40:
                box1.style.top = box1.offsetTop + step + 'px';
                break;
        }
    }, 30);

    document.onkeydown = function(e) {
        if (e.shiftKey) {
            step = 30;
        } else {
            step = 5;
        }
        dir = e.keyCode;
    };

    document.onkeyup = function() {
        dir = 0;
    };
}
```
- 设置一个全局变量：方向dir，先定义不赋值
  - 用于各个函数之间调用这个变量
- 当键盘按钮按下时，获取键盘的方向键赋值给方向dir变量
- 设置一定定时器，每30ms检查一次，方向键是否按下，如果匹配好方向键则执行下面的switch函数，如果没有匹配，则每30ms检查完结束
- 添加按键抬起事件，按键松开后，将方向设置为0，或者其他四个方向键之外的数字
       
将见按键事件和运动事件分开，则不会出现卡顿现象
       
       
       
       
       
       
       
       
       
       
       
       
       
       
       
       
       
