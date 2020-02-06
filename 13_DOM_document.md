
# DOM ducument

文档节点元素查询 

1. `document.body;`，获取body标签
2. `document.documentElement;` 获取html根标签
3. `document.all;`，获取全部标签

根据class查询元素
1. `document.getElementsByClassName`，css的class name，IE8+

2. `document.querySelector('.box1 div')`，很强大，css选择器的方式，返回满足条件的第一个对象
```html
var div = document.querySelector('.box1 div');
console.log(div.innerHTML);

<div class="box1">
        <div>box1 content</div>
</div>
```

3. `document.querySelectorAll`，返回所有满足css选择器条件的对象
```html
var div = document.querySelectorAll('.box1');
console.log(div);

<div class="box1">
    <div>1st content</div>
</div>
<div class="box1">
    <div>2nd content</div>
</div>
```
<img width="323" src="https://user-images.githubusercontent.com/26485327/73938666-b0136c00-4922-11ea-833e-cc4bd88768f1.png">

# DOM 增删改

### 1. 子节点-父节点
点击按钮后，在页面添加一个选项。在<div id="checkbox">在添加一个checkbox input
        
1. 创建一个标签元素`document.createElement('div');`
2. 创建一个文本元素`document.createTextNode('add new text');`
3. 将文本元素添加为标签元素的子元素`父节点.appendChild(new_text);`
        

```html
<script>
window.onload = function(){
    function clickBtn(id, func) {
        var btn = document.getElementById(id);
        btn.onclick = func;
    }；
    clickBtn('addbtn', function() {
        var div_add = document.getElementById('add');
        var new_input = document.createElement('div');
        var new_text = document.createTextNode('add new text');

        new_input.appendChild(new_text);
        div_add.appendChild(new_input);
    });
}
</script>

<div id="add">
    <button id="addbtn">Add element</button>
</div>
```
- appendChild 不能添加元素在form表单里面。新添加元素会闪一下，就就消失了。但是可以调整其他参数来显示
        - https://blog.csdn.net/sinat_27088253/article/details/51316760


4. `父节点.insertBefore(新添加节点，旧节点)`，同一个父节点下，添加新节点到已有节点之前

```html
<script>
window.onload = function(){
    function clickBtn(id, func) {
        var btn = document.getElementById(id);
        btn.onclick = func;
    }；
    clickBtn('addbtn', function() {
        var div_add = document.getElementById('add');
        var add_btn = document.getElementById('addbtn');

        var new_input = document.createElement('div');
        var new_text = document.createTextNode('add new text');

        new_input.appendChild(new_text);
        div_add.insertBefore(new_input, add_btn);
    });
}
</script>

<div id="add">
    <button id="addbtn">Add element</button>
</div>
```

5. `父节点.replaceChild(新添加节点，被替换节点)`，替换子节点

6. `父节点.removeChild(子节点)`，删除子节点
        - **`子节点.parentNode.removeChild()`，更常用。**通过当前节点，获取其父节点，在通过父节点找到其下面的其他子节点。这样就不用单独去获取一个元素的父节点了

7. `div_add.innerHTML += '<div>new text</div>'`，最最简单，直接添加innerHTML，但是这种方式消耗太大。因为需要替换掉原来的html代码，天健一部分新代码后，在拼接上原来的，组成新的插入ducoment。根据实际情况和上面的appendChild结合使用

```javascript
window.onload = function(){
    function clickBtn(id, func) {
        var btn = document.getElementById(id);
        btn.onclick = func;
    }；
    clickBtn('addbtn', function() {
        var div_add = document.getElementById('add');
        div_add.innerHTML += '<div>new text</div>';
        
        // var add_btn = document.getElementById('addbtn');

        // var new_input = document.createElement('div');
        // var new_text = document.createTextNode('add new text');

        // new_input.appendChild(new_text);
        // div_add.insertBefore(new_input, add_btn);
    });
}
```
