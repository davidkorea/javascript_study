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

判断输入数值是否为质数，质数只能被1和自己整除，1不是质数也不是和数
```javascript
do {
    var num = +prompt('input a number bigger than 1 : ');
} while (num <= 1)

var flag = true;

for (var i = num - 1; i > 1; i--) {
    console.log(i);
    if (!(num % i)) {   // 没有余数（num % i = 0），则说明被除了1和本身以外其他数字整除，不是质数
        flag = false;   // num % i = 0）=false，需要将该条件转换为true，在设置标识位
    }                   // 或者使用 if( num % i == 0 )
}
if (flag) {
    alert('Yes');
} else {
    alert('No');
}
```
- 将输入的数字和1之外的其他数字找出来，依次做除法。如果有能被整出的数字出现，则该输入数值不是质数
- if (!(num % i))
- if (num % i == 0)


打印✳️方块矩阵
```
*   *   *   *   *   
*   *   *   *   *   
*   *   *   *   *   
*   *   *   *   *   
*   *   *   *   *   
```
```javascript
var num = 5;

for (i = 1; i <= num; i++) {
    for (j = 1; j <= num; j++) {
        document.write('*&nbsp;&nbsp;&nbsp;');
    }
    document.write('</br>')
}
```
- `&nbsp;`，为空格





打印斜三角

```javascript
var num = 5
for (var i = 1; i <= num; i++) {
    for (var j = 1; j <= i; j++) {
        document.write('*');
    }
    document.write('</br>')
}
```
```
*
**
***
****
```

```javascript
var num = 5;

for (i = 1; i <= num; i++) {
    for (j = num; j >= i; j--) {
        document.write('*&nbsp;&nbsp;&nbsp;');
    }
    document.write('</br>')
}
```
```
*   *   *   *   
*   *   *   
*   *   
*   
```

九九乘法表
```javascript
for (var i = 1; i <= 9; i++) {
    for (var j = 1; j <= i; j++) {
        document.write(i, 'x', j, '=', i * j, ' ');
    }
    document.write('</br>')
}
```
```
1x1=1
2x1=2 2x2=4
3x1=3 3x2=6 3x3=9
4x1=4 4x2=8 4x3=12 4x4=16
5x1=5 5x2=10 5x3=15 5x4=20 5x5=25
6x1=6 6x2=12 6x3=18 6x4=24 6x5=30 6x6=36
7x1=7 7x2=14 7x3=21 7x4=28 7x5=35 7x6=42 7x7=49
8x1=8 8x2=16 8x3=24 8x4=32 8x5=40 8x6=48 8x7=56 8x8=64
9x1=9 9x2=18 9x3=27 9x4=36 9x5=45 9x6=54 9x7=63 9x8=72 9x9=81
```
```javascript
<script>
for (var i = 1; i <= 9; i++) {
    for (var j = 1; j <= i; j++) {
        document.write('<span>', i, 'x', j, '=', i * j, '</span>');
    }
    document.write('</br>')
}
</script>

<style>
    span {
        display: inline-block;
        width: 70px;
    }
</style>
```
<img width="1066" alt="截屏2020-02-01下午2 50 12" src="https://user-images.githubusercontent.com/26485327/73588313-7f869900-4502-11ea-9375-ad2efc75ba82.png">






