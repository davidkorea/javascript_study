# javascript_study

每个浏览器都有自己实现JavaScript的引擎，如Chrome的V8引擎，Firefox的spidermonkey引擎，Safari的JavaScriptCore

## js and es

`es ≈ js`
- javascript 编程语言
- ECMAscript 技术标准，Netscape最初创造了JavaScript语言后，捐献给了欧洲计算机制造商协会（European Computer Manufacturers Association）开源

完整的JavaScript由3部分构成
1. ECMAScript，标准
2. DOM，document object model，操作网页
3. BOM，browser object model，操作浏览器

## Usage
### 1. Script
```javascript
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title></title>
    <script type="text/javascript">
      // javascript code here
    </script>
  </head>
  <body>
    
  </body>
</html>
```
### 2. Tag Attribute
标签属性，结构与行为强耦合，不方便后期维护，不推荐使用
```javascript
  <body>
    <button onclick="alert('welcome');">Click</button>
    
    <a href="javascript:alert('link');">Click link</a>
    <a href="javascript:;">blank link</a>    
  </body>
```
- 点击按钮时，弹窗
- 点击超链接时，弹窗
- 点击超链接，空白相应

### 3. 引用外部文件
create `script.js`file in the same folder with html file

```javascript
<script type="text/javascript" src="script.js"> 

</script>
```
- 一旦引用外部文件，就不能再在script标签带写代码了，即使写了也不会执行，仅执行外部代码
- 如需要内部js代码，则需要再另行创建一个<script>标签来书写内部代码
- js代码从上往下顺序执行，需注意外部、内部代码执行顺序


## Rules
1. 每条js语句后要加分号`;`，虽然不写，浏览器会自行补全并运行，但影响效率
2. 通过`var`来定义和赋值变量 `var age = 10;`，规范使用驼峰命名法`firstName`
    - 类似python，js无需要在定义变量时定义数据类型的动态语言
    - `console.log(typeof age);` 通过`typeof `函数查看变量类型
3. 6种数据类型， 基本数据类型String，Number，Boolean，Null，Undefined 以及 引用数据类型Object
    - String
      - 单引号，双引号嵌套
      - 需要显示引号，或特殊字符时，转义字符`\`+ 单引号或双引号
        - `\n`换行
        - `\t`制表符
        - `\\`斜线
    - Number
      - js可以表示的最大数`console.log(Number.MAX_VALUE);` 1.7976931348623157e+308
      - js可以表示的最小数`console.log(Number.MIN_VALUE);` 5e-324 但这也是大于0的最小正数，而不是负数
      - 超过上述最大值时，返回`Infinity`正无穷，Infinity本身也是数值型，`-Infinity`为负无穷
        ```javascript
        var a = Infinity;
        console.log(typeof a); 
        // return number
        ```
      - `NaN` 也是数值型 Not a number
        ```javascript
        var a = NaN;
        console.log(typeof a); 
        // return number
        ```
      - 进行浮点型数值运算时，可能得到不准确数值，因为计算机无法用二进制精确表示十进制的十分之一，但其他语言有纠偏机制，而js没有
        ```
        var c = 0.1 + 0.2;
        console.log(c);
        // return 0.30000000000000004
        ```
    - Boolean
      ```javascript
      var bool = true;
      console.log(typeof bool);
      // return boolean
      ```
    - Null 空值，是一个对象类型
      ```javascript
      var a = null;
      console.log(typeof a);
      // return object
      ```
    - Undefined 未定义，当声明一个变量，且不给变量赋值时，该变量为undefined
      ```jaavscript
      var x;
      console.log(x);
      // return undifined
      ```

4. 强制类型转换
    - **转换为string**
      - `toString()`方法，Null和Undefined没有此方法
        ```javascript
        var x = 123;
        var y = x.toString();
        console.log(typeof x);
        console.log(typeof y);
        // return number
        // return string
        ```
        - `toString()方法不改变原变量的数值类型`
        - 可是使用`a = a.toString()`来覆盖掉原变量的数据类型
      - `String()`函数，可以将null和undefined直接转换为字符串“null”和“undefined”
        ```javascript
        var x = null;
        var y = String(x);
        console.log(typeof x);
        console.log(typeof y);
        // return object
        // return string
        ```
    - **转换为number
      - `Number()`函数**
        - 字符串中只有数字
          ```javascript
          var a = "123";
          console.log(typeof a);
          var b = Number(a);
          console.log(typeof b);
          // return string
          // return number
          ```
        - 字符串中含有字母，则转换为`NaN`
          ```javascript
          var a = "1aa23";
          var b = Number(a);
          console.log(typeof b);
          console.log(b);
          // return number
          // return NaN
          ```
        - 空字符串`""`,`"    "`转换为数值`0`
          ```javascript
          var a = "";
          var b = Number(a);
          console.log(typeof b);
          console.log(b);
          // return number
          // return 0
          ```
        - boolean
          - true -> 1
          - false -> 0
        - null -> 0
        - undefiend -> NaN
      - 数字+字符串，转数值`parseInt()`,`parseFloat()`
        ```javascript
        var a = "123.45 px";
        var b = parseInt(a);
        var c = parseFloat(a);
        console.log(b);
        console.log(c);
        // return 123
        // return 123.45
        ```
        - `"a123 bc"`不实用，转换为NaN，只适用于数字开头的字符串
        - 非字符串值，如boolean值会先转换为字符串再转换为数字，那么true -> NaN
        
        
      
    - **转换为boolean**




















