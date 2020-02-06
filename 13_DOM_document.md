
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

点击按钮后，在页面添加一个选项。在<div id="checkbox">在添加一个checkbox input
- 创建一个标签元素`document.createElement('div');`
- 创建一个文本元素`document.createTextNode('add new text');`
- 将文本元素添加为标签元素的子元素`父节点.appendChild(new_text);`
        

```html
window.onload = function(){
    function clickBtn(id, func) {
        var btn = document.getElementById(id);
        // console.log(btn.value);
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


<div id="add">
    <button id="addbtn">Add element</button>
</div>
```
- appendChild 不能添加元素在form表单里面。新添加元素会闪一下，就就消失了。但是可以调整其他参数来显示
        - https://blog.csdn.net/sinat_27088253/article/details/51316760















