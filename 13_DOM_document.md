
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
