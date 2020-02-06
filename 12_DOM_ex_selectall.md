

## 1. 实现按钮功能
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

代码优化 
```javascript
// reverse
clickBtn('reverse', function() {
    var allBox = document.getElementsByName('items');
    for (i = 0; i < allBox.length; i++) {
        // if (allBox[i].checked) {
        //     allBox[i].checked = false;
        // } else {
        //     allBox[i].checked = true;
        // }
        
        allBox[i].checked = !allBox[i].checked     
    }
});
```
- 直接取反，而无需通过if判断当前值



## 2. 增加功能
- 增加一个勾选按钮checkbox
   - [x] 点选后，全选下面选项
   - [] 取消勾选后，取消全选下面选项
- 手动勾选下面选项
   - 当全部勾选时，新增checkbox被自动勾选
   - 未全部勾选是，新增checkbox不被勾选
- 按钮
   - select all -> 自动勾选checkbox
   - select no -> 自动取消勾选checkbox
   - reverse -> 当且仅当所有选项被勾选时，自动勾选checkbox，否则不勾选
   

![Feb-06-2020 17-34-39](https://user-images.githubusercontent.com/26485327/73924211-15596400-4907-11ea-9f65-3f424278c55f.gif)


```html
<html>
<head>
    <style>
        * {
            margin: 10;
            padding: 0;
        }
    </style>
    <script>
        window.onload = function() {
            var checkallbox = document.getElementById('checkall');
            var allBox = document.getElementsByName('items');

            // 1. Checkbox
            // check and show status of all checkbox

            checkallbox.onclick = function() {
                for (i = 0; i < allBox.length; i++) {
                    allBox[i].checked = this.checked;
                    // you checked then all checked
                    // you unchecked,then all unchecked
                }
            };

            function chkboxclick(id) {
                var chkbox = document.getElementById(id);
                chkbox.onclick = function() {
                    for (i = 0; i < allBox.length; i++) {
                        checkallbox.checked = true;
                        if (!allBox[i].checked) {
                            checkallbox.checked = false;
                            break;
                        }
                    }
                };
            };

            list = ['run', 'swim', 'football', 'basketball'];
            for (i = 0; i < list.length; i++) {
                chkboxclick(list[i]);
            };


            // 2. Button
            // click button function wrap up
            function clickBtn(id, func) {
                var btn = document.getElementById(id);
                console.log(btn.value);
                btn.onclick = func;
            }

            // slect all btn
            clickBtn('selectall', function() {
                for (i = 0; i < allBox.length; i++) {
                    allBox[i].checked = true;
                }
                checkallbox.checked = true;
            });
            // select no
            clickBtn('selectno', function() {
                for (i = 0; i < allBox.length; i++) {
                    allBox[i].checked = false;
                }
                checkallbox.checked = false;
            });

            // reverse
            clickBtn('reverse', function() {
                for (i = 0; i < allBox.length; i++) {
                    allBox[i].checked = !allBox[i].checked;
                };

                for (i = 0; i < allBox.length; i++) {
                    checkallbox.checked = true;
                    if (!allBox[i].checked) {
                        checkallbox.checked = false;
                        break;
                    }
                };

            });

            // post
            clickBtn('post', function() {
                var postlist = [];
                for (i = 0; i < allBox.length; i++) {
                    if (allBox[i].checked) {
                        postlist.push(allBox[i].value)
                    };
                }
                if (postlist.length > 0) {
                    alert('Posted.\n' + postlist);
                } else {
                    alert('please select.')
                }
            });
        }
    </script>
</head>

<body>
    <form method="POST">
        Your favorate <input type="checkbox" id="checkall">Select all/no
        <br>
        <input type="checkbox" name="items" value="run" id="run">Run
        <input type="checkbox" name="items" value="swim" id="swim">Swim
        <input type="checkbox" name="items" value="football" id="football">Football
        <input type="checkbox" name="items" value="basketball" id="basketball">Basketball
        <br>
        <input type="button" id="selectall" value="Select All">
        <input type="button" id="selectno" value="Select No">
        <input type="button" id="reverse" value="Reverse">
        <input type="button" id="post" value="Post">
    </form>
</body>
</html>
```























