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
### 2. Exanples
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
### 2.1 Basic
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
        
        
```javascript
for(var i = 0; i < 10; i++){
  alert(i);
}
```
```javascript
var i = 0;

for(;i<10;){
  alert(i++);
}
```
```javascript
for(;;){          // 死循环
  alewrt'hello');
}
```
  
### 2.2 Examples
        
1～100奇数求和
```javascript
var sum = 0;

for (i = 1; i <= 100; i++) {
    if (i % 2 == 1) {
        sum += i;
    }
}
console.log(sum);
```

1～100所有7的倍数的和
```javascript
for (i = 1, sum = 0; i <= 100; i++) {
    if (i % 7 == 0) {
        // console.log(i);
        sum += i;
    }
}
console.log('\n', sum);
}
```

所有3位的水仙数，如1^3 + 5^3 + 3^3 = 153
```javascript
// 1^3 + 5^3 + 3^3 = 153, 3 digits
for (var x = 0; x < 10; x++) {
    for (var y = 0; y < 10; y++) {
        for (var z = 0; z < 10; z++) {
            var sum = 0;
            sum += 100 * x + 10 * y + z;
            if (x ** 3 + y ** 3 + z ** 3 == sum && sum > 100) {
                console.log(x, y, z, '-----', sum);
            }
        }
    }
}
```

```javascript
for (var i = 100, x, y, z; i < 1000; i++) {
    x = parseInt(i / 100);            // 取整parseInt，舍去小数
    y = parseInt((i - x * 100) / 10);
    z = i - x * 100 - y * 10;
    if (x ** 3 + y ** 3 + z ** 3 == i) {
        console.log(x, y, z, '-----', i);
    }
}
// 1 5 3 ----- 153
// 3 7 0 ----- 370
// 3 7 1 ----- 371
// 4 0 7 ----- 407
```





        
