- 在for循环里面，当自己本身的事件函数里面调用自己时，必须使用this

# 1. 增加删除表格信息

> **函数的创建，要以事件为基础，所有获取元素对象的操作，都要在事件函数里面创建。不能以批量处理的for循环思路来创建**

- delete删除当前行信息
- submit体检新信息

![Feb-07-2020 15-22-17](https://user-images.githubusercontent.com/26485327/74009240-c6223a80-49bd-11ea-8e14-b8a20ee16e7e.gif)


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
            // 1. delete
            function delEmployee() {
                var del = document.getElementsByTagName('a');
                for (i = 0; i < del.length; i++) {     // add onclick function for every <a>link
                    del[i].onclick = function() {
                        var tr = this.parentNode.parentNode;    // this代指当前被点击的delete连接             
                        var name = tr.getElementsByTagName('td')[0].innerText;
                        var flag = confirm('Delete? ' + name);   
                        if (flag) {
                            tr.parentNode.removeChild(tr);
                        }
                    }
                }
            };
            delEmployee();


            // 2. add
            var clickBtn = document.getElementsByTagName('button')[0]
            clickBtn.onclick = function() {
                // get name,email,phone element
                var nameInput = document.getElementById('emName');
                var emailInput = document.getElementById('email');
                var phoneInput = document.getElementById('phone');

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
                delEmployee(); 
                // 之前是页面加载时就有的delete动作，而那时候还没有新增
                // 要想新增后也有删除动作，需要再次执行删除函数
            }
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
            <!-- 点击一个超链接后，会自动调转，不论是否设定href，跳转后，旧不能执行js代码 -->
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
## 1.1 删除功能
1. 获取删除超链接元素
2. 创建单击事件函数
    1. 通过for循环为获取到的所有超链接元素，绑定onclick函数
        - 注意！！！这里面要使用this来获取当前`<a>`标签下的父元素或子元素。这一点太重要了，看下面详细说明
    2. 弹出确认提示框 confirm提示框有确认和取消刘昂个按钮，分别返回true和false
    3. 确认则删除行，注意使用**`自己.父节点.删除子节点(自己)`**的方式最为简单
    
3. 注意该删除功能的函数可以放在window.onload()的外面，不需要等到加载页面时在加载
    - 定义好一个函数，但是不调用这个函数，则不会由于页面加载顺序而导致报错


### - 细说 this
```html
<html>
<head>
    <script>
        window.onload = function() {
            var allBtn = document.getElementsByTagName('button');
            for (i = 0; i < allBtn.length; i++) {
                allBtn[i].onclick = function() {
                  // 自己本身的onclick函数中，没法使用自己
                    alert(allBtn[i]);               // undefined
                    alert(allBtn[i].innerText);     // no action
                  // 自己本身的onclick函数中，要想使用自己，需要使用this                  
                    alert(this);                    // [object HTMLButtonElement]
                    alert(this.innerText);          // click1,click2,click3
                }
            }
        };
    </script>
</head>

<body>
    <div id="btnDiv">
        <button id="btn">Click1</button>
        <button id="btn">Click2</button>
        <button id="btn">Click3</button>
    </div>
</body>
</html>
```
- **对于for循环里面的每个对象，在自己的事件函数里面，打印自己本身，调用自己本身，必须使用this**
- 因为，页面加载完成window.load后，会立即运行for循环，但是里面的onclick函数，只有按钮被点击时才被执行
- 当响应函数执行的时候，for循环早就已经执行完了
- 因此每次点击按钮，都是在for执行完所有元素循环之后的一个index，而这个index无法匹配对应的元素
    - 如下图，一共3个按钮，加载页面的时候按钮序号0，1，2就已经循环完毕，即allBtn[0]，allBtn[1]，allBtn[2]
    - 当真正点击按钮时，index已经是3，但是并没有序号3对应的元素，也因此alert()会显示undefined，因为确实没有allBtn[3]

![Feb-07-2020 16-54-58](https://user-images.githubusercontent.com/26485327/74014983-b826e680-49ca-11ea-8b2f-2b5ff29f5259.gif)

```javascript
window.onload = function() {
    var allBtn = document.getElementsByTagName('button');
    for (i = 0; i < allBtn.length; i++) {
        alert('for loop is running: ' + i)
        allBtn[i].onclick = function() {
            alert('event function is running: ' + i)
        }
    }
};
```


## 1.2 对于添加功能
1. 首先要获取submit按钮元素，在点击该按钮后，在<table>下面新添加一个行<tr>
2. 设置该按钮的点击事件函数
    1. 分别找到每个input输入框的输入内容，因为时自闭标签，`元素.value`即可获取输入内容
    2. 分别创建tr，td，a，text元素，并拼接
    3. 最后拼接到table下面
        - 注意！！`父节点.appendChild(单一参数)`，一次只能添加一个参数，不能多参数！！！
        - 注意！！虽然html源代码中没有，但是浏览器自动把多个`<td>`放到一个`<tbody>`标签下
        - 为了css样式能够正常套用，也需要将上面新创建的元素添加到浏览器生成的`<tbody>`标签下
        - `<tbody>`标签元素按照正常方式获取即可
    4. 执行tbody.appendChild(new)即可
3. 如果上面创建的删除函数实在window.onload里面，此处新增行之后，需要重新调用
    - 因为时刚毅加载页面，就已经调用的delete函数，而在那之后，才新增加的行元素，新增加的删除超链接元素不在删除函数获取的范围之内

-----

# 2. 代码优化

- 问题很明显，新建一行，需要创建很多元素节点以及输入内容的文本节点，拼接工作量太大
- 但是直接`table.innerHTML += newElement`，会全部写入新的以及旧的内容
- 因此，结合上述两点
    - 创建一个新的tr
    - `tr.innerHTML += new`，行里的诸多标签节点和文本节点直接手写html代码
    - 添加时，仅将tr添加值tbody里面


```javascript
// add
var clickBtn = document.getElementsByTagName('button')[0]
clickBtn.onclick = function() {
    // get the input of name,email,phone element
    var nameInput = document.getElementById('emName').value;
    var emailInput = document.getElementById('email').value;
    var phoneInput = document.getElementById('phone').value;

    var table = document.getElementById('employeeTable');
    var tr = document.createElement('tr');

    tr.innerHTML = "<td>" + nameInput + "</td>" +
        "<td>" + emailInput + "</td>" +
        "<td>" + phoneInput + "</td>" +
        "<td><a href='javascript:;'>delete</a></td>";

    // broswer will create a <tbody>
    var tbody = document.getElementsByTagName('tbody')[0];
    tbody.appendChild(tr);
    delEmployee(); 
}
```



