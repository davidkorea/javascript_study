
# DOM css 

# 1. 更改样式
- `元素.style.CSS属性`，可更改样式，但是新的样式会直接加载到html的标签上，而不是修改css文件
- 因为html标签上的样式优先级高，可以覆盖掉css文件的设定值，但是当css文件里面设定了`!important`，内联样式无法覆盖css文件
- 通过此方法获取css数值，野味**内联样式**，而不是css文件里面的样式设定的当前样式
- 如果没有内联样式，`元素.style.CSS属性`将获取空值

<img width="926"  src="https://user-images.githubusercontent.com/26485327/74025548-27a6d100-49df-11ea-8a00-e9bbdb80e46b.png">

```html
<html>
<head>
    <style>
        #box1 {
            width: 200;
            height: 200;
            background-color: blue !important;
        }
    </style>
    <script>
        window.onload = function() {
            var btn = document.getElementById('btn');
            var box = document.getElementById('box1');

            btn.onclick = function() {
                box.style.height = '300px';
                box.style.width = '300px';
                box.style.backgroundColor = 'red';
            };
        }
    </script>
</head>

<body>
    <div id="box1"></div>
    <button id="btn">click</button>
</body>
</html>
```
- css中的属性`-`，需要通过驼峰方式来哦表示

# 2. 读取当前样式值
读取当前显示的样式的值，也不是css的也不一定时内建样式，谁生效，获取谁的值

一下方法为只读，不可以通过其进行属性值的设定，修改必须通过style进行

1. `对象.currentStyle.height`，仅IE支持
2. `getComputedStyle(box, null);`，window属性，可直接调用，返回一个style对象，需要什么样式属性，在该对象中查找
    - **对于css没有设置的属性，将返回当前的实际值大小**

```javascript
var btn2 = document.getElementById('btn2');
btn2.onclick = function() {
    var obj = getComputedStyle(box, null);
    alert(obj.backgroundColor);
}
```

对于需要同时兼容IE8以及其他浏览器的时候，需要同事实现
```javascript
 btn2.onclick = function() {
if (window.getComputedStyle) {
    alert(getComputedStyle(box, null).width);
    } else {
        alert(box.currentStyle.width);
    }
}
```
- if里面需要`window.getComputedStyle`，这样表示为window对象的一个属性，若没有则返货false
- if里面仅填写`getComputedStyle`，表示为变量，若果函数作用域和全局作用域都找不到改变量，那么报错，而不是返回false

<img width="411" src="https://user-images.githubusercontent.com/26485327/74028944-86bc1400-49e6-11ea-9973-0bbf2051eabf.png">

代码优化
```javascript
function getStyle(element, styleAttr) {
    return window.getComputedStyle ? getComputedStyle(element, null)[styleAttr] : element.currentStyle[styleAttr]
}
```
- `return expression1?expression2:expression3`
- 如果1，那么2，否则3


3. `对象.clientWidth`，`对象.clientheight`获取的属性值，没有像素单位，只有数字。
    - 不仅如此，clientwidth还可以显示padding，但是不包括框border

```html
<style>
    #box1 {
        width: 200;
        height: 200;
        padding: 10px;
        border: 10px blueviolet solid;
        background-color: blue;
    }
</style>

<script>
var btn2 = document.getElementById('btn2');
        btn2.onclick = function() {
            alert(box.clientWidth);
        }
</script>
```
<img width="432" src="https://user-images.githubusercontent.com/26485327/74029382-8a9c6600-49e7-11ea-8b42-c6a61935dee1.png">


4. `offsetWidth`, `offsetHeight`，偏移量，可以获取包括边框border的数值，也没有px，仅数值

5. `offsetParent`，定位父元素，返回离当前元素最近的开启了定位`position: relative;`的外围元素，只要position你不是static就有事开启了定位
    - 如果所有祖先元素都没开启定位，则返回body
    
6. `offsetLeft`, `offsetTop`，当前元素相对于定位元素（offsetParent）的水平偏移量和垂直偏移量

7. `scrollWidth`，`scrollHeight`，可以获取元素整个滚动区域的宽度和高度，clientWidth和clientHeight只可以获取课件区域的大小，而非元素的完整大小
8. `scrollLeft`，`scrollTop`，水平滚动条，举例左边界滚动的举例。垂直滚动条，举例顶部滚动的举例
    - 当垂直滚动条到底时，`scrollHeight - scrollTop = clientHeight`
    - 当水平滚动条到后时，`scrollWidth - scrollLeft = clientWidth`
    - 应用场景就是，注册时，用户条款全部月丹完成后，就是滚动条拉倒底后，才能继续注册















