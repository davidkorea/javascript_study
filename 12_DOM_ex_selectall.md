

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
   - [ ] 取消勾选后，取消全选下面选项
- 手动勾选下面选项
   - 当全部勾选时，新增checkbox被自动勾选
   - 未全部勾选是，新增checkbox不被勾选
- 按钮
   - select all -> 自动勾选checkbox
   - select no -> 自动取消勾选checkbox
   - reverse -> 当且仅当所有选项被勾选时，自动勾选checkbox，否则不勾选
   
思路
1. 因为当选项勾选框全部都被勾选时，【全选】勾选框也要被自动勾选上，因此要绑定事件在每一个选项勾选框
2. 当前这个选项勾选框被点击后，还要检查其他选项框是否也全部被勾选，如是，则需要点亮【全选】
3. 全选状态下，若有个一选项被取消后，【全选】也要被自动熄灭
4. 除了上面的勾选框要动作之外，下面的按钮也要跟着动作，全选是点亮，否则熄灭
5. 需要单独考虑的是反选按钮，有两种情况
   - 全被勾选，全不被勾选，都好处理
   - 部分勾选情况，需要每个选项框的状态都检查一遍，再决定【全选】是否点亮
   
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
         var checkallbox = document.getElementById('checkall');   // 【全选】勾选框
         var allBox = document.getElementsByName('items');        //  所有选项勾选框

         // 1. Checkbox
         // check and show status of all checkbox

         checkallbox.onclick = function() {              // 当【全选】被勾选时，选项也全被勾选
             for (i = 0; i < allBox.length; i++) {
                 allBox[i].checked = this.checked;       // 作为checkallbox的方法onclick调用
             }                                           // this代指checkallbox   
         };

         function chkboxclick(id) {                      // 每个选项勾选框的点击事件函数
             var chkbox = document.getElementById(id);   // 根据id获取勾选框对象
             chkbox.onclick = function() {
                 for (i = 0; i < allBox.length; i++) {   // 当一个勾选框被点击后，默认【全选】选框被勾选
                     checkallbox.checked = true;         // 如果执行if，那么【全选】状态会被更改，否则全选
                     if (!allBox[i].checked) {           // 但，其他选项选框如果有一个没被勾选
                         checkallbox.checked = false;    // 则将【全选】选框取消勾选
                         break;
                     }
                 }
             };
         };

         list = ['run', 'swim', 'football', 'basketball'];
         for (i = 0; i < list.length; i++) {             // 将每个选项选框的id放到数组中
             chkboxclick(list[i]);                       // 循环数组，以使每个选框被点击时，执行上面的函数
         };


         // 2. Button
         // click button function wrap up
         function clickBtn(id, func) {
             var btn = document.getElementById(id);
             btn.onclick = func;
         }

         // slect all btn
         clickBtn('selectall', function() {
             for (i = 0; i < allBox.length; i++) {
                 allBox[i].checked = true;
             }
             checkallbox.checked = true;        // 点击按钮后，各选项选框和【全选】选框，都要被勾选
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
                 allBox[i].checked = !allBox[i].checked;  // 是的当前的选中状态和之前取反，不同
             };

             for (i = 0; i < allBox.length; i++) {        // 选项选框变化后，【全选】选框也要响应
                 checkallbox.checked = true;              // 和上面思路一样，默认【全选】开启
                 if (!allBox[i].checked) {                // 有一个选项选框没被勾选，【全选】也不勾选
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
        <input type="checkbox" name="items" value="run" id="run">Run       // 为每个选框增加id属性
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























