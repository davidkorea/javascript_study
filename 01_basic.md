
JavaScript代码从上往下，顺序执行

## 输出语句

```javascript
<script type="text/javascript">
  alert("pop up message window in browser.")
  document.write("write in html body tag.")
  console.log("show mesg in console")
</script>
```
- 浏览器弹窗
- html <body> 标签中，即网页中插入内容
- F12 Console中显示内容


## 运算符
运算符都会返回一个结果
- `typeof`， 返回值是一个字符串
- 算数运算符
  - 任何值和NaN计算，结果都是NaN
  - true + 1 = 2
  - true + null = 1
  - 123 + "abc" = "123abc"，任何值与字符串相加，相当于字符串拼接
    - 用于长字符串换行后拼接
    - 数字+空字符串`""`，用于将数值型转换为字符型
    - `console.log("result = " + )`
      ```javascript      
      var result = 123
      console.log("result = ", result);
      console.log("result = " + result);
      ```
      ![image](https://user-images.githubusercontent.com/26485327/72709824-0bb2cb00-3ba9-11ea-8cb3-868061b9203c.png)

