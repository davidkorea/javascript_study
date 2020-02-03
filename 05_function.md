
- 函数也是一个对象
- 对象object是将一组属性放在一个塑料袋
  - `var obj = new Object();`
- 函数function是将一个功能封装起来，方便其他函数进行调用
  - `var func = new Function();`
  - 对象具有的功能函数也全都具有
  - 但是一般是使用构造函数的方式创建一个函数对象，而是使用函数声明或者函数表达式来创建一个函数  
  
  
# 1. 创建函数
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


# 2. 函数的参数
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
  - 实参也可以是一个函数，因为函数也是一个对象，对象的功能，函数也全都具有
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
    - 使用 函数名，就是调用函数本身
    - 使用 函数名()，就是使用函数的返回值

# 3. 返回值
- 返回值可以是任意类型，当然也可以返回一个函数
- 有时候一个函数的计算结果需要传递给其他函数使用，而不是console.log来显示。需要return将函数结果传递出来，通过一个变量来接收一个函数的返回结果
- 函数中return后面的语句将不再执行，此处可以和break和continue进行比较
- 如果函数中没有return语句，将返回undefined


### 比较return， break， continue
```javascript
function hello() {
    alert('start');
    for (i = 0; i < 5; i++) {
        if (i == 2) {
            break;              // start -> 0 1 -> finish
            continue;           // start -> 0 1 3 4 -> finish
            return;             // start -> 0 1
        }
        console.log(i);
    }
    alert('finish');
}

hello();
```
- break 结束整个循环，执行循环后的语句
- continue 结束本次循环，继续下一个循环
- return 结束整个函数，return后面的语句不在执行

### 函数嵌套且返回值是一个函数
```JavaScript
function fun1() {
    function fun2() {
        console.log('hello fun2');
    }
    return fun2
}

fun1()();   // hello fun2
```
- fun1函数的返回值是fun2函数本身，注意不是fun2()函数2的返回值，由于没指明默认是undefined，
- 执行fun1()，就是执行fun1的返回值，也就是fun2
- 再加一个()，fun1()()，就是执行fun2()


# 4. 立即执行函数
适用于仅执行一次的函数
```javascript
( function(参数){语句} )()；
```

```javascript
( function(a, b) {
    console.log(a + b);
} )(1, 2)；   // 3
```

# 5. 对象的方法
- 对象的属性，是一个单一变量类型，str，num，bool
- 对象的方法，是一个函数

```javascript
var obj = new Object();
obj.name = 'plus';            // 对象的属性
obj.sum = function(a, b) {    // 对象的方法
    return a + b;
};

obj.sum(1, 2);    // 3

// 枚举一个对象中的属性和方法
for (var i in obj) {          
    console.log('key: ', i, ' --- value: ', obj[i]);
}
// 取出对象属性的值的时候，因为i是变量，需要通过方括号[]来取出变量的值，而不能用点.的方式
```
```
// return
key:  name  --- value:  plus
key:  sum  --- value:  ƒ (a, b) {
            return a + b;
        }
```
- console.log()就是调用console的log方法
- 调用一个对象的方法，就是调用一个函数
- 通过for...in...枚举一个对象中的属性和方法


# 6. 作用域
## 6.1 全局作用域
- 全局作用域的代码直接在页面<script>标签下，页面打开时创建，页面关闭时销毁
  - 全局作用域中的变量，称作全局变量
- 全局作用域中有一个全局对象window，代表一个浏览器窗口，由浏览器默认创建
  ```javascript
  console.log(window);
  // Window {parent: Window, opener: null, top: Window, length: 0, frames: Window, …}
  ```
- 在全局作用域中创建的变量，都会作为全局对象window的属性保存，而创建的函数都将作为全局对象window的方法保存
  ```javascript
  var a = 10;
  console.log(window.a);    // 10
  ```
  
- **变量声明提前**
  - 所有使用var关键字声明的变量，会在所有代码运行之前被程序声明，无论var在程序的哪一行，但不会赋值
    ```javascript
    console.log(a);   // undefined
    var a = 10;       // 因为使用var关键字，所以所有代码运行前，程序已经生命了变量，只是没有赋值
    ```
    就相当于
    ```javascript
    var a;
    console.log(a);
    a = 10;
    ```

- **函数声明提前**
  - 使用函数声明的形式创建的函数，function 函数名(){...}，在程序代码运行之前，就被默认创建
    - 因此可以在函数声明之前来调用该函数
  - 使用函数表达式创建的函数，var func = function(){...}，在程序运行之前，仅创建了var声明的变量，并没有赋值
    - 因此不能在声明函数之前调用该函数
    ```javascript
    fun1();
    fun2();

    function fun1() {
        console.log('hi, fun1');
    }

    var fun2 = function() {
        console.log('hi, fun2');
    };
    ```
    <img width="423" alt="截屏2020-02-02下午5 52 25" src="https://user-images.githubusercontent.com/26485327/73606393-cea4fa80-45e4-11ea-989d-85b734440cc6.png">
    



## 6.2 函数作用域
- 调用函数时，创建函数作用域，函数执行完毕时销毁
- 每调用一次函数，就创建一个新的函数作用域，且相互独立
- 在函数中操作一个变量时，有限寻找函数内部的变量，如果不存在，则向上一级作用域寻找，直到找到全局作用域中不存在该变量，则报错
- 当函数作用域中和函数作用域中有相同变量a，且在函数中想调用全局变量，可以使用windows.a
- 函数作用域中的**变量声明提前**，同上，函数中的代码运行之前，var关键字声明的变量首先呗声明，但并不赋值
  - 函数中不实用关键字var声明的变量，就是全局变量，相当于window.变量，会覆盖原有全局变量的值
    ```javascript
    var a = 10;

    function fun1() {
        a = 22;
        console.log('inner: ', a);
    }
    
    fun1();                       // 22
    console.log('outer: ', a);    // 22
    ```
    <img width="332" alt="截屏2020-02-02下午6 15 39" src="https://user-images.githubusercontent.com/26485327/73606692-05c8db00-45e8-11ea-8b22-4d76d72e6dca.png">
    
        
    ```javascript
    var a = 10;
    function fun1() {
        b = 22;           //  没有关键字var，则为全局变量，相当于window.变量
    }
    fun1();
    console.log('b: ', b);
    ```
    <img width="270" alt="截屏2020-02-02下午7 54 40" src="https://user-images.githubusercontent.com/26485327/73607804-db7e1a00-45f5-11ea-904b-e4c6b6fbcd50.png">
- 定义了形参，相当于声明了函数定义域的变量
  ```javascript
  var e = 10;
  function fun1(e) {
      console.log(e);
  }
  fun1();       // 此处()中没有传递实参，所以对应函数内部就是声明了变量，但没有赋值
  // undefined
  ```
  <img width="248" alt="截屏2020-02-02下午8 13 12" src="https://user-images.githubusercontent.com/26485327/73608011-72e46c80-45f8-11ea-84dd-351c28edfc9b.png">
  
  ```javascript
  var a = 10;

  function fun1(a) {
      console.log(a);       // undefined,因为调用函数时，没有传递实参
      a = 22;               // 因为有形参，相当于定义了局部变量，此时不实用var，也是复制给局部变量，不影响外部变量
  }
  fun1();
  console.log(a);           // 10
  ```

- 函数作用域中的**函数声明提前**，同上，函数中的代码运行之前，`function 函数名(){...}`会被首先创建，而`var func = function(){...}`仅声明一个变量名，不会赋值后面的函数


# 7. debug
```javascript
alert(d);

var a = 10;
var b = 20;
c = 30;

function func() {
    console.log('hello');
}
var d = 40;
```
<img width="902" alt="截屏2020-02-02下午8 44 57" src="https://user-images.githubusercontent.com/26485327/73608352-e12b2e00-45fc-11ea-829a-bb495772bd0d.png">
- 需要手动添加需要视器的变量大搜监视器watch


# 8. this
解析器在调用函数时，每次都会想函数内部传递一个隐藏参数this，该参数称作 **函数执行的上下文**
- this是由浏览器传递给函数内部的一个参数
- 根据函数调用的方式不同，this指代的也不同
    1. 函数调用时，this指代window
    2. 方法调用时，谁调用，this指代谁
- 实际上，上述两点也是一样的，因为调用函数fun()就是调用window.fun()，而window调用了该函数，this就是window
```javascript
function func() {
    console.log(this);
}

var obj = {
    name: 'david',
    methodFun: func
}

console.log(func == obj.methodFun);   // true 二者完全一样

func();             // this = window
obj.methodFun();    // this = obj
```
<img width="714" alt="截屏2020-02-02下午9 23 29" src="https://user-images.githubusercontent.com/26485327/73608806-45042580-4602-11ea-8aa4-a22c4149afb8.png">

举例，存在多个对象，当调用对象的一个方法时，该方法自动输出该对象的name属性的值
- 因为每个对象都需要实现这个功能，所以单独写好一个函数，来供每个对象中的方法来调用
- 因为每个对象需要显示其自己的name属性，因为这个功能函数里面不能写死name变量，二十根据谁调用，显示谁的原则来实现

```javascript
var name = 'global name'

function func() {
    console.log(name);      // 因为此处写死了name
}                           // 无论对象方法调用还是函数调用都是返回全局变量的值

var obj1 = {
    name: 'david',
    method: func
}
var obj2 = {
    name: 'korea',
    method: func
}

func();
obj1.method();
obj2.method();
```
<img width="340" alt="截屏2020-02-02下午9 49 43" src="https://user-images.githubusercontent.com/26485327/73609163-ee004f80-4605-11ea-9fc8-df0cc31de924.png">


改用this来进行指代
```javascript
var name = 'global name'

function func() {
    console.log(this.name);      // this.name，谁调用，显示谁的name属性的值
}                          

var obj1 = {
    name: 'david',
    method: func
}
var obj2 = {
    name: 'korea',
    method: func
}

func();
obj1.method();
obj2.method();
```
<img width="273" alt="截屏2020-02-02下午9 50 07" src="https://user-images.githubusercontent.com/26485327/73609168-fc4e6b80-4605-11ea-8e35-bfe1340624f4.png">

再如，批量创建对象
```javascript
var obj1 = {
    name: 'david,
    age: 18,
    method: function() {
        alert(this.name);
    }
}

var obj2 = {
    name: 'korea',
    age: 18,
    method: function() {
        alert(this.name);
    }
}

...
```

```javascript
function create(name, age) {
    var obj = {
        name: name,
        age: age,
        method: function() {
            alert(this.name);
        }
    }
    return obj;
}

var obj1 = create('david', 22);
console.log(obj1);
obj1.method();

var obj2 = create('korea', 18);
console.log(obj2);
obj2.method();
```
<img width="415" alt="截屏2020-02-02下午10 17 10" src="https://user-images.githubusercontent.com/26485327/73609553-c4492780-4609-11ea-98fa-796cad6809bb.png">
