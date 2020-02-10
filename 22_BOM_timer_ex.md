
# 计时器综合项目
1. 点击按钮，box1向右移动👉


# 1. 点击按钮，box1向右移动
- `box1.style.left = 100px;`，只可以变更一次元素位置，不能连续改变
  - 因此需要一个定时器，来每10ms自动走100px，来实现连续运动效果
- 位置增大
  - `步长++`的方式每次走1px，这样速度固定，每走一步都是1px
  - 当前的位置`box1.offsetLeft`上增加一个固定的步长，这样速度可以由步长来改变
  
```html
<script>
      window.onload = function() {
          // 1. box1 move right
          var btn1 = document.getElementById('btn1');
          var box1 = document.getElementById('box1');
          var step = 5;
          btn1.onclick = function() {
              var timer1 = setInterval(() => {
                  var oldValue = box1.offsetLeft;
                  step++;
                  box1.style.left = oldValue + step + 'px';
                  if (oldValue >= 800) {
                      clearInterval(timer1);
                  }
              }, 30);
          }
      }
  </script>
</head>

<body>
    <button id="btn1">box1 forward</button>
    <button id="btn2">box1 backward</button>
    <div id="box1" class="box"></div>
    <div id="box2" class="box"></div>
    <div id="line"></div>
</body>
```
### 改进：提高函数通用性
- 向右，向左操作合在一个函数里面
- 元素样式的更改不只是变更offsetLeft，还要适应更改height，width等属性




