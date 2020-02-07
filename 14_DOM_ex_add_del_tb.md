# 增加删除表格信息

- delete删除当前行信息
- submit体检新信息

```html
<html>
<head>
    <style>
        table {
            border-collapse: collapse;
            width: 500px;
            line-height: 30px;
            text-align: center;
        }
        
        table,
        table tr th,
        table tr td {
            border: 1px solid;
        }
    </style>
    <script>
        window.onload = function() {
            // delete
            function delEmployee() {
                var del = document.getElementsByTagName('a');
                console.log(del.length);
                for (i = 0; i < del.length; i++) {
                    del[i].onclick = function() {
                        var tr = this.parentNode.parentNode; // <a> 's parent <tr>
                        // alert('Delete?'); // alert canot cancel,find another window's method
                        var name = tr.getElementsByTagName('td')[0].innerText;
                        var flag = confirm('Delete? ' + name); // has cancel and confirm
                        if (flag) {
                            tr.parentNode.removeChild(tr);
                        }
                    }
                }
            };
            delEmployee();
            // 该函数是页面加载就运行了，可是这时候还没有执行下面的add
            // 所以下面新增的不会有delete动作


            // add
            var clickBtn = document.getElementsByTagName('button')[0]
            clickBtn.onclick = function() {
                // get name,email,phone element
                var nameInput = document.getElementById('emName');
                var emailInput = document.getElementById('email');
                var phoneInput = document.getElementById('phone');

                // nameInput.value, emailInput.value, phoneInput.value
                var table = document.getElementById('employeeTable');
                var tr = document.createElement('tr');

                var td1 = document.createElement('td')
                var input1 = document.createTextNode(nameInput.value);
                td1.appendChild(input1);

                var td2 = document.createElement('td')
                var input2 = document.createTextNode(emailInput.value);
                td2.appendChild(input2);

                var td3 = document.createElement('td')
                var input3 = document.createTextNode(phoneInput.value);
                td3.appendChild(input3);

                var td4 = document.createElement('td')
                var alink = document.createElement('a');
                alink.href = 'javascript:;'
                var alink_text = document.createTextNode('delete');
                alink.appendChild(alink_text);
                td4.appendChild(alink);

                // tr.appendChild(td1, td2, td3); !!!! cannot multi paras
                tr.appendChild(td1);
                tr.appendChild(td2);
                tr.appendChild(td3);
                tr.appendChild(td4);

                // broswer will create a <tbody>
                var tbody = document.getElementsByTagName('tbody')[0];
                tbody.appendChild(tr);
                // alert(input1);
                delEmployee(); //  之前是页面加载时就有的delete动作，而那时候还没有新增
                // 要想新增后也有删除动作，需要再次执行删除函数
            }


            // 以onclick事件为单位 创建函数。不能以批量的思维创建！！！！

        }
    </script>
</head>

<body>
    <table id="employeeTable">
        <tr>
            <th>Name</th>
            <th>Email</th>
            <th>Phone</th>
            <th>Option</th>
        </tr>
        <tr>
            <td>Bom</td>
            <td>tom@hi.com</td>
            <td>01012345678</td>
            <td><a href="javascript:;">delete</a> </td>
        </tr>
        <tr>
            <td>Aom</td>
            <td>tom@hi.com</td>
            <td>01012345678</td>
            <!-- <td><a href="./adddelemployee.html">delete</a> </td> -->
            <!-- 否则超链接会跳转，不能执行js代码 -->
            <td><a href="javascript:;">delete</a> </td>

        </tr>
    </table>


    <div id="formDiv">
        <h4>Add new</h4>

        <table>
            <tr>
                <td class="word">Name</td>
                <td id="input"><input type="text" name="emName" id="emName"></td>
            </tr>
            <tr>
                <td class="word">Email</td>
                <td id="input">
                    <input type="text" name="email" id="email">
                </td>
            </tr>
            <tr>
                <td id="word">Phone</td>
                <td class="input">
                    <input type="text" name="phone" id="phone">
                </td>
            </tr>
            <tr>
                <td colspan="2" align="center">
                    <button id="addBtn" value="abc">Submit</button>
                </td>
            </tr>
        </table>
    </div>
</body>

</html>
```
对于删除功能
1. 获取删除超链接元素
2. 创建单击事件函数
    - 找到该delete按钮所在行元素
    - 弹出确认提示框 confirm提示框有确认和取消刘昂个按钮，分别返回true和false
    - 确认则删除行，注意使用**`自己.父节点.删除子节点(自己)`**的方式最为简单
    
3. 注意该删除功能的函数可以放在window.onload()的外面，不需要等到加载页面时在加载
    -















