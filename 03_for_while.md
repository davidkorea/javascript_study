# 1. `while`
### 1. Basics
- `while(){}`，先判断，再执行
- `do{}while()`，先执行，后判断。保证循环体至少执行一次

```javascript
var i = 0;

while (i < 10) {
  i++;
  document.write(i, '</br>');
}
```
1. 初始化一个变量
2. 设置一个条件表达式
3. 更新初始变量


```javascript
var i = 0;

do {
    document.write(i++, '</br>')
} while (i < 10);
```
### 2. Exanp[les
存款1000，年利率5%，存多少年后金额为5000
```javascript
var money = 1000;
var i = 0;
while (money < 5000) {
    money *= 1.05
    i++;
}
alert(i);
// 33
```

输入错误时，持续提示弹窗，输入合法是则继续执行
```javascript
do {
    var score = +prompt('input score 0-100: ');
}
while (score > 100 || score < 0);

if (score > 60) {
    alert('pass');
} else {
    alert('failed');
}
```





# 2. `for`

```javascript
for(初始化变量; 条件表达式; 更新初始变量){
  语句；
}
```
1. 初始化一个变量
2. 判断一个条件表达式
3. 执行循环体语句
4. 更新初始变量
    - 再次判断条件表达式
    - 再次执行循环体
    - 再次更新初始变量
        - 判断条件表达式
        - ...
        
        
        
        
        
        
        
        
        
