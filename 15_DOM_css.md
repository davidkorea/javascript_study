
# DOM css 

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





















