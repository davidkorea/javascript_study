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































