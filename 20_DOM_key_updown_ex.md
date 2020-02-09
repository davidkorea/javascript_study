
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

### 练习：上下左右按键控制移动放线
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

  
