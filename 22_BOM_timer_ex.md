
# 计时器综合项目
1. 点击按钮，box1向右移动👉
2. 点击按钮，box1向左移动



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
## 改进：提高函数通用性
元素样式的更改不只是变更offsetLeft，还要适应更改height，width等属性
- **使用getComputedStyle，`getComputedStyle(box1, null).left` == `box1.offsetLeft`，二者功能一样，offsetLeft没有单位px，而前者有**
- [15_DOM_css_ex.md#2-读取当前样式值](https://github.com/davidkorea/javascript_study/blob/master/15_DOM_css_ex.md#2-读取当前样式值)
- 适配所有浏览器
  ```javascript
  function getStyle(element, style) {
      if (window.getComputedStyle) {
          return getComputedStyle(element, null)[style];  // chrome
      } else {
          return element.currentStyle[style];             // IE
      }
  }

  var left = getStyle(box1, 'left');
  alert(left);
  ```
  - 此时返回的数值带有单位px，需要只保留数字，`parseInt(getStyle(box1, 'left'))`
    ```html
    <style>
        #line {
            height: 1000px;
            width: 0px;
            border-left: 1px solid;
            position: absolute;
            /* 开启position定位，才能设置位置，否则下面不生效!!!!!!!!!!!!!!!!!!!! */
            top: 0px;
            left: 800px;
        }

    </style>
    <script>
        function getStyle(element, style) {
            if (window.getComputedStyle) {
                return getComputedStyle(element, null)[style];
            } else {
                return element.currentStyle[style];
            }
        }

        window.onload = function() {
            // 1. box1 move right
            var btn1 = document.getElementById('btn1');
            var box1 = document.getElementById('box1');
            btn1.onclick = function() {
                var timer1 = setInterval(() => {
                    var step = 100;

                    var oldValue = parseInt(getStyle(box1, 'left'));
                    var newValue = oldValue + step;

                    box1.style.left = newValue + 'px';
                    if (newValue >= 800) {
                        clearInterval(timer1);
                    }
                }, 30);
            }
        }
    </script>
    ```
- **问题1**：当步长step是一个奇怪的数字，比如11，13，17等，不会在定时器走的过程中整整好好等于800
  - 如果想要box1正好停在800px线上，需要强制设定大于800的话，就等于800
    ```diff
    btn1.onclick = function() {
        var timer1 = setInterval(() => {
            var oldValue = parseInt(getStyle(box1, 'left'));
            var newValue = oldValue + step;

    +       if (newValue > 800) {
    +           newValue = 800;
    +       };
            
            box1.style.left = newValue + 'px';
            if (newValue == 800) {
                clearInterval(timer1);
            };
        }, 30);
    }
    ```
- **问题2**：当多次点击按钮后，多个定时器会被触发，而所有定时器都是给box1的，那么box1的速度聚会不断增加。而且新定时器会覆盖旧定时器，关闭定时器只能关闭最后一个，之前的无法关闭
  - 同一个元素的定时器开始之前，先关闭这个元素上之前的定时器。按下按钮开始移动时，首先先关闭之前定时器
  - 需要把定时器变量设置为全局变量，否则内层函数serinterval()的timer1变量无法在外层函数onclick()中被调用。全局定义变量，局部赋值变量
    ```diff  
    + var timer1
      btn1.onclick = function() {
    +    clearInterval(timer1);

    -    var timer1 = setInterval(() => {
    +    timer1 = setInterval(() => {
            var oldValue = parseInt(getStyle(box1, 'left'));
            var newValue = oldValue + step;

            if (newValue > 800) {
                newValue = 800;
            };
            box1.style.left = newValue + 'px';
            if (newValue == 800) {
                clearInterval(timer1);
            };
        }, 30);
    ```
### 代码
![Feb-10-2020 16-21-15](https://user-images.githubusercontent.com/26485327/74132370-6330dd80-4c21-11ea-8e54-5b21b4e10278.gif)

```html
<head>
    <script>
        function getStyle(element, style) {
            if (window.getComputedStyle) {
                return getComputedStyle(element, null)[style];
            } else {
                return element.currentStyle[style];
            }
        }

        window.onload = function() {
            // 1. box1 move right
            var btn1 = document.getElementById('btn1');
            var box1 = document.getElementById('box1');
            var timer1
            btn1.onclick = function() {
                clearInterval(timer1);

                timer1 = setInterval(() => {
                    var step = 10;

                    var oldValue = parseInt(getStyle(box1, 'left'));
                    var newValue = oldValue + step;

                    if (newValue > 800) {
                        newValue = 800;
                    };
                    box1.style.left = newValue + 'px';

                    if (newValue == 800) {
                        clearInterval(timer1);
                    };
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
  
  
  
# 2. 点击按钮，box1向左移动

```javascript
btn1.onclick = function() {
  ...
};

btn2.onclick = function() {
    clearInterval(timer1);
    timer1 = setInterval(() => {
        var step = -10;                     // 步长改为负值

        var oldValue = parseInt(getStyle(box1, 'left'));
        var newValue = oldValue + step;

        if (newValue < 0) {                 // 回到0点 
            newValue = 0;
        };
        box1.style.left = newValue + 'px';

        if (newValue == 0) {
            clearInterval(timer1);
        };
    }, 30);
}
```
  
## 改进：提高函数通用性
 
- 可以看查干湖btn1和btn2的大部分代码都是一样的，因此创建一个函数来统一使用

```javascript
function getStyle(element, style) {
    if (window.getComputedStyle) {
        return getComputedStyle(element, null)[style];
    } else {
        return element.currentStyle[style];
    }
}

window.onload = function() {
    // btn, button
    // box, element to be moved 
    // style, left, height, innerWidth 
    // step, 10, 50 
    // destination, 0 or 800

    var timer1;

    function moveBox(btn, box, style, step, destination) {
        // var timer1; 下一次调用该函数，复发取消之前函数里面的定时器
        // 因为每次调用该函数，都创建一个定时器，你的函数不能关闭群殴他人函数内的定时器

        var btn = document.getElementById(btn);
        var box = document.getElementById(box);
        btn.onclick = function() {
            clearInterval(timer1);

            timer1 = setInterval(() => {
                var oldValue = parseInt(getStyle(box, style));
                console.log(oldValue);

                if (destination == 800) {
                    var newValue = oldValue + step;
                } else if (destination == 0) {
                    var newValue = oldValue - step;
                }

                if (newValue >= 800) {
                    newValue = 800;
                } else if (newValue <= 0) {
                    newValue = 0;
                };

                box.style[style] = newValue + 'px';

                if (newValue >= 800 || newValue <= 0) {
                    clearInterval(timer1);
                }
            }, 30);
        };
    };

    moveBox('btn1', 'box1', 'left', 10, 800);
    moveBox('btn2', 'box1', 'left', 10, 0);
}
```
  
  









