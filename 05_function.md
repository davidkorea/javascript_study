
- 函数也是一个对象
- 对象object是将一组属性放在一个塑料袋
  - `var obj = new Object();`
- 函数function是将一个功能封装起来，方便其他函数进行调用
  - `var func = new Function();`
  - 对象具有的功能函数也全都具有
  - 但是一般是使用构造函数的方式创建一个函数对象，而是使用函数声明或者函数表达式来创建一个函数
  
  
# 创建函数
### 函数声明
```javascript
function 函数名([形参1，形参2...]){
  语句...
}           // 声明一个函数可以不加分好

函数名(实参1, 实参2...)；  //  调用函数
```

### 函数表达式

```javascript
var 函数名 = function(){
  语句...
}；          // 因为是赋值语句，末尾加分好

函数名();    //  调用函数
```
- 将一个匿名函数赋值给一个变量


# 函数的参数
- 形参
- 实参
```javascript
function sum(a, b) {
    console.log(a + b);
}

sum(2, 3, true, 'hello');    // 5
sum(2);     // NaN
```
- 解析器不会检查实参的变量类型
- 解析器也不会检查实参的个数
  - 当实参个数超过形参个数时，超过的实参将被忽略
  - 当实参个数少于形参个数时，返回NaN，因为缺少的参数为undefined
- 实参可以是任何变量类型
  - 当函数的参数过多时，可以讲参数打包到一个对象中
  - 实参也可以是一个函数
    ```javascript
    function people(o) {
        console.log('i am ', o.name, ',', o.age, ' years old.');
    }
    
    var obj = {
        name: 'david',
        age: 18
    };
    
    people(obj);        
    // i am  david , 18  years old.
    
    function myFunc(a){
        a(obj);           // 就相当于people(obj);
    } 
    myFunc(people);       // 实参是一个函数，所以形参a就是一个函数，可以调用a(obj);
    // i am  david , 18  years old.
    ```

# 返回值
- 有时候一个函数的计算结果需要床底给其他函数使用，而不是console.log来显示
- 需要return将函数结果传递出来，通过一个变量来接收一个函数的返回结果
- 函数中return后面的语句将不再执行
- 如果函数中没有return语句，将返回undefined

判断偶数
```javascript
function oushu(num) {
    return num % 2 == 0;
}

var res = oushu(3);
console.log(res);   //  flase
```

计算圆的面积
```
function sqr(r) {
    return Math.PI * r * r
}
var res = sqr(1);
console.log(res);
```







