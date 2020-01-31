
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

### 加法运算
- 任何值和NaN计算，结果都是NaN
- true + 1 = 2
- true + null = 1
- 123 + "abc" = "123abc"，任何值与字符串相加，相当于字符串拼接
  - 用于长字符串换行后拼接
  - 用于将数值型转换为字符型
    - 数字+空字符串`""`
    - `a = +"18"` -> 18
  - `console.log("result = " + )`
    ```javascript      
    var result = 123
    console.log("result = ", result);
    console.log("result = " + result);
    ```
    ![image](https://user-images.githubusercontent.com/26485327/72709824-0bb2cb00-3ba9-11ea-8cb3-868061b9203c.png)

  - `var a = 1 + 2 + "3"` -> "33"
  - `var a = "1" + 2 + 3` -> "123"
  - `var a = 1 + 2 + +"3"` -> 6, 因为加号将字符串转换为了数字
  
### 减法运算
- `var a = 100 - true` -> 99
- `var a = 100 - false` -> 100
- `var a = 100 - "2"` -> 98
- `var a = 100 - "a"` -> NaN


### 乘除法
- `var a = 2 * "2"` -> 4
- `var a = 2 * null` -> 0
- `var a = 2 / true` -> 2
- `var a = 2 / null` -> Infinity
- `var a = 2 / false` -> Infinity
- `var a = 2 / NaN` -> NaN

### 取余数

- `var a = 9 / 3` -> 0，9除以3得3余0
- `var a = 9 / 4` -> 1，9除以4得2余1

### 自增自减
变量和表达式不同
- 变量 `var a = 1;`
- 表达式 `a++;`，`++a;`

#### `a++`
```javascript
var a = 1;
console.log(a++);
console.log("a = ",a);
```
![image](https://user-images.githubusercontent.com/26485327/72712517-8d592780-3bae-11ea-93d8-6de464f313bc.png)
- 表达式`a++`的返回值是 原变量的值
- 表达式执行后表示为原变量自增1且赋值回给原变量`a = a + 1`

```javascript
var a = 1;
var b = a++;
console.log("b = ", b);
console.log("a = ", a);
// b = 1, a = 2
```
![image](https://user-images.githubusercontent.com/26485327/72713423-5d128880-3bb0-11ea-94c1-3d4bc5bed96d.png)
- 表达式返回值为 自行前的原变量值
- 但是表达式，实际上已经执行了自增1并复制给了原变量，原变量已经变成了2

#### `++a`
```javascript
var a = 1;
console.log(++a);
console.log("a = ",a);
```
![image](https://user-images.githubusercontent.com/26485327/72712684-e1fca280-3bae-11ea-8bb5-ef913a329155.png)
- 表达式`++a`的返回值是 自增后的数值

那么，
```javascript
var a = 1;
var result = a++ + ++a + a;
console.log("a = ", a);
console.log("result = ", result);
// a= 3, result = 7
```
![image](https://user-images.githubusercontent.com/26485327/72713829-11141380-3bb1-11ea-99e2-4cf8342b2e00.png)
- 表达式a++ -> 1, 执行表达式后，变量值a = 2
- 表达式++a -> 3, 执行表达式后，变量值a = 3
- result = 1 + 3 + 3

```javascript
var a = 1;
a = a++;
console.log(a);
// return a=1
```
- because `a++` equals the origin value of `a`, so `a++` is still 1.
- when excute the expression `a++` the value of `a` is 2. 
- then set a = 1 again








