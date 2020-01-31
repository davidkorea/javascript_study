
# 1. `if...else if...else`
```javascript
if(条件表达式1){
  多条语句; 
  ...
}else if(条件表达式2){
  多条语句;
  ...
}else{
  多条语句;
  ...
}
```

### 1. Basics

```javascript
var a = 10;
if (a > 10 && a < 20)       // only &&, NO and
  alert('> 10');
  alert("hello");
```
- 当`if(条件表达式)`中的条件表达式的运算结果为真，则执行紧随其后的第一条语句
- if条件不满足，则其后面的第一条语句不执行，之后的语句则按顺序执行

```javascript
var a = 10;
if (a > 10)
{
  alert('> 10');
  alert("hello");
}
```
- 将if后的全部语句都放在一个代码块中，可以改善上述情况
- 但是`{}`代码块并不是必须，推荐如此使用

### 2. Exanples

输入三个整数，输出排序后的三个数字

```javascript
var num1 = +prompt("input integer1: ");   // + 类型转换 string->number
var num2 = +prompt("input integer2: ");
var num3 = +prompt("input integer3: ");

alert("pls confirm your input: " + num1 + ", " + num2 + ", " + num3);

if (num1 > num2 && num1 > mun3) {
    if (num2 > num3) {
        alert("num1 > num2 >num3")
    } else {
        alert("num1 > num3 >num2")
    }
} else if (num3 > num1 && num3 > num2) {
    if (num1 > num2) {
        alert("num3 > num1 > num2")
    } else {
        alert("num3 > num2 > num1")
    }
} else {
    if (num1 > num3) {
        alert("num2 > num1 > num3")
    } else {
        alert("num2 > num3 > num2")
    }
}
```
- **`prompt()`函数的返回值类型为string，通过加号`+`将其输入值转换为数值类型**

# 2. `switch...case`
### Basic
```javascript
switch(条件表达式){
  case 表达式数值1:
    语句;
    break;
  case 表达式数值2:
    语句;
    break;
  default:
    语句;
    break;
}
```
- 依次比较switch的条件表达式与case表达式的值
- 当且仅当switch的条件表达式与case表达式全等时，执行该case下面的语句
- 执行完case下的语句后，`break;`跳出该case并结束switch函数
  - 若没有`break;`则执行万当前case后，将后面所有case都执行
  - 注意⚠️，每个case语句后面都要有`break;`
- 不满足所有case时，执行default

### Examples
输入数字，输出对应星期
```javascript
var num = +prompt('input a integer: ');   // change str to num by plus +

switch (num) {
    case 1:
        alert('Mon');
        break;
    case 2:
        alert('Tue');
        break;
    case 3:
        alert('Wed');
        break;
    case 4:
        alert('Thu');
        break;
    case 5:
        alert('Fri');
        break;
    default:
        alert('Nan');
        break
}
```

高于60分输出合格，否则输出不合格
```javascript
var score = 77;
cond = score > 60;        // my thought
switch (cond) {
    case true:
        alert('pass');
        break;
    default:
        alert('failed');
        break;
}
```
- 通过新增一个变量来判断是否大于60
```javascript
var score = 99.5;
switch (true) {           // no need to use a new var
    case score > 60:      // if `score>60` is true and is the same as `switch true`
        alert('pass');
        break;
    default:
        alert('failed');
        break;
}
```
- 无需新增变量
- 当case表达式的结果和switch表达式的结果完全一致时，执行该case
- 直接使用if即可








