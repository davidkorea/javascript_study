
# 计时器综合项目
1. 点击按钮1，box1向右移动
2. 点击按钮2，box1向左移动
3. 点击按钮3，box2向右移动



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
- **问题**：虽然统合到一个函数里面，但是里面的条件判断0和800还是写死了
  
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
    // box, element to be moved -
    // style, left, height, innerWidth -
    // step, 10, 50 
    // destination, 0 or 800

    var timer1;

    function moveBox(btn, box, style, step, destination) {
        var btn = document.getElementById(btn);
        var box = document.getElementById(box);
        btn.onclick = function() {
            clearInterval(timer1);

            var currentValue = parseInt(getStyle(box, style));
            // dest 800, 元素的位置都会小于等于dest，step>0
            // dest 0，元素位置都会大于等于dest，step<0
            
            if (currentValue >= destination) {
                step = -step;
            }

            timer1 = setInterval(() => {
                var oldValue = parseInt(getStyle(box, style));
                var newValue = oldValue + step;

                // if (destination == 800) {
                //     var newValue = oldValue + step;
                // } else if (destination == 0) {
                //     var newValue = oldValue - step;
                // }

                if ((step > 0 && newValue >= destination) || (step < 0 && newValue <= destination)) {
                    newValue = destination;
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


# 3. 点击按钮2，box2向右移动

```javascript
moveBox('btn3', 'box2', 'left', 10, 800);
```

![Feb-10-2020 19-54-37](https://user-images.githubusercontent.com/26485327/74147954-43101700-4c3f-11ea-8737-e3da625b8c0c.gif)


- box1移动时，box2会停止。一个运动，那么另一个会自动停止
  - 因为不同元素box1和box2都通过同一个函数moveBOX绑定离开同一个定时器
  - 然而定时器时timer1定义在了外层作用域，每次新调用moveBox函数，都是给这个外层作用域变量timer1赋值
  - 当moveBox函数被新调用时，首先会操作清除定时器，也因此box2执行时会停止box1运动
  - 需要给每个moveBox函数绑定不同的定时器
    - **将定时器设置为每个对象的一个属性**，只要是对象object，就可以给其添加一个属性，即使这个对象不是自行创建的对象

![Feb-10-2020 20-12-51](https://user-images.githubusercontent.com/26485327/74149049-caf72080-4c41-11ea-8a55-cca69e3e3e15.gif)

```javascript

function moveBox(btn, box, style, step, destination) {
    var btn = document.getElementById(btn);
    var box = document.getElementById(box);

    btn.onclick = function() {
        clearInterval(box.timer1);              // 关闭当前对象的定时器，而不会关闭其他对象的定时器

        var currentValue = parseInt(getStyle(box, style));
        if (currentValue >= destination) {
            step = -step;
        }

        box.timer1 = setInterval(() => {        // 把timer设置为对象的属性，即给box对象添加一个timer属性
            var oldValue = parseInt(getStyle(box, style));
            var newValue = oldValue + step;

            if ((step > 0 && newValue >= destination) || (step < 0 && newValue <= destination)) {
                newValue = destination;
            };

            box.style[style] = newValue + 'px';

            if (newValue >= 800 || newValue <= 0) {
                clearInterval(box.timer1);      // 关闭定时器，也是关闭对应对象的定时器
            }
        }, 30);
    };
};
```















