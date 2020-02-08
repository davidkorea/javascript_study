
# addEventLisener & attachEvent

同时为一个元素的**同一个事件**添加多个响应函数

- 使用`元素.onclick = function(){}`的方式，下面的函数盖掉前面的函数，因此只会执行对后面一个响应函数
- 适用`元素.addEventLisener("click", function(){}, false)`，三个参数，但是后面的addEventLisener不会覆盖掉前面的addEventLisener，而是所有的addEventLisener都会依次执行
  - addEventLisener中的this，代指调用addEventLisener的元素
- IE8及以下不支持addEventLisener，可以使用`attachEvent('onclick', function(){})`，两个参数，执行顺序为从后往前
  - attachEvent中的this，代指window
  
## 1. addEventLisener()
- onclick -> click，事件名称没有on

```html
<script>
    window.onload = function() {
        var btn = document.getElementById('btn');

        // click to add new link
        // btn.onclick = function() {
        //     alert(1);
        // };
        // btn.onclick = function() {
        //     alert(2);
        // };

        btn.addEventListener('click', function() {
            alert(1);
        }, false);
        btn.addEventListener('click', function() {
            alert(2);
        }, false)
    };
</script>

<body>
    <button id="btn">click</button>
</body>
```
  
  
  
## 2. 兼容所有浏览器
自建函数来兼容所有浏览器，满足元素的多事件同时触发
1. 被触发的元素
2. 触发方式，onclick，onscroll，onmousemove
3. 回调函数callback
4. 统一this

```javascript
function bindEvent(obj, event, callback) {
    if (obj.addEventListener) {
        obj.addEventListener(event, callback, false);
    } else {
        obj.attachEvent('on' + event, callback);
    }
}

bindEvent(btn, 'click', function() {
    alert(1);
});
bindEvent(btn, 'click', function() {
    alert(2);
});
```
- IE8及以下，显示顺序为 2 —> 1
- chrome和firefox，显示顺序 1 -> 2

接下来，统一this
- this指代谁，是由调用方式决定的
- 此处由于时函数调用`obj.attachEvent('on' + event, callback);`，callback函数调用
- 但是callback函数是浏览器调用的，我们控制不了，如果我们能3，则需要使用`callback.call(obj)`这种方式来修改函数的this
- 此时，我们不再使用callback函数来让浏览器调用，而是自行写一个匿名函数，此时将触发匿名函数，再在匿名函数中调用callback函数

```diff
- obj.attachEvent('on' + event, callback);
+ obj.attachEvent('on' + event, function(){
    callback.call(obj);
  });
```
- 此时this就是obj了















