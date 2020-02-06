
1. 全选
2. 全不选
3. 反选
4. 提交

![Feb-06-2020 12-03-17](https://user-images.githubusercontent.com/26485327/73904976-be3c9a80-48d8-11ea-9241-7da68018ebe8.gif)

```html
<html>
<style>
    * {
        margin: 10;
        padding: 0;
    }
</style>
<head>
    <script>
        window.onload = function() {
            function clickBtn(id, func) {
                var btn = document.getElementById(id);
                console.log(btn.value);
                btn.onclick = func;
            }

            // slect all btn
            clickBtn('selectall', function() {
                var allBox = document.getElementsByName('items');
                for (i = 0; i < allBox.length; i++) {
                    allBox[i].checked = true;
                }
            });
            // select no
            clickBtn('selectno', function() {
                var allBox = document.getElementsByName('items');
                for (i = 0; i < allBox.length; i++) {
                    allBox[i].checked = false;
                }
            });

            // reverse
            clickBtn('reverse', function() {
                var allBox = document.getElementsByName('items');
                for (i = 0; i < allBox.length; i++) {
                    if (allBox[i].checked) {
                        allBox[i].checked = false;
                    } else {
                        allBox[i].checked = true;
                    }
                }
            });

            // post
            clickBtn('post', function() {
                var allBox = document.getElementsByName('items');
                var postlist = [];
                for (i = 0; i < allBox.length; i++) {
                    if (allBox[i].checked) {
                        postlist.push(allBox[i].value)
                    };
                }
                alert('Posted.\n' + postlist);
            });
        }
    </script>
</head>

<body>
    <form method="POST">
        Your favorate
        <br>
        <input type="checkbox" name="items" value="run">Run
        <input type="checkbox" name="items" value="swim">Swim
        <input type="checkbox" name="items" value="football">Football
        <input type="checkbox" name="items" value="basketball">Basketball
        <br>
        <input type="button" id="selectall" value="Select All">
        <input type="button" id="selectno" value="Select No">
        <input type="button" id="reverse" value="Reverse">
        <input type="button" id="post" value="Post">
    </form>
</body>
</html>
```
