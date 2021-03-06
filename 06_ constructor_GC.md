# 构造函数，用于创建对象的函数

- 构造函数，就是用于创建对象Object的函数
- 一个函数前面使用new关键字，那么该函数就是构造函数，反之不使用new，那么该函数就是普通函数
- this
    1. 以函数形式调用，this代指window
    2. 以对象的方法调用，this代指该对象，谁调用指代谁
    3. 构造函数形式调用，this代指自动新创建的对象实例

-----
# 1. 工厂方法批量创建对象

```javascript
function person(name, age) {
    var obj = new Object();
    obj.name = name;
    obj.age = age;
    obj.method = function() {
        alert('hi, person');
    }
    return obj;
}

function dog(name, age) {
    var obj = new Object();
    obj.name = name;
    obj.age = age;
    obj.method = function() {
        alert('wolf wolf')
    }
    return obj
}

var obj1 = person('david', 22);
console.log(obj1);

var obj2 = dog('korea', 18);
console.log(obj2);
```
<img width="476" alt="截屏2020-02-03下午2 46 14" src="https://user-images.githubusercontent.com/26485327/73631446-f3a47680-4693-11ea-85e0-66c4b767f104.png">

- 虽然两个函数一个是person，一个是dog，但是二者的proto都是Object，不好区分
- 那如果我想让他们不显示Object，而是显示自定义的person或是dog呢？

# 2. 构造函数批量创建对象
使用构造函数，类似于python的class
- 创建一个构造函数，和创建一个普通函数并没有什么不同
- 构造函数调用时需要使用关键字new,因为new可以实现，在调用函数时，立即创建一个对象
- 构造函数创建事，函数名首字母默认大写
```javascript
function Person() {
    alert(this);
}
var obj = new Person();
console.log(obj);
```
<img width="359" alt="截屏2020-02-03下午2 54 25" src="https://user-images.githubusercontent.com/26485327/73631829-13886a00-4695-11ea-8f31-f02bea7dcd8b.png">

1. new关键字会自动在堆内存中开辟一块空间，换句话说就是自动创建一个对象，由解析器（浏览器）实现
    - `var obj = new Person();`，obj就是自动被创建的对象
2. 将自动创建的对象设置为函数的this，也就是说，在构造函数中可以通过this来引用新创建的对象
    - `alert(this);`，其中this代指上面自动创建的obj对象
3. 逐行执行函数代码
4. 将这个自动创建的对象作为返回值返回

```javascript
function Person(name, age) {
    this.name = name;                   // 表示把传入的name值，赋值给新建的那个对象的name属性
    this.age = age;
    this.method = function() {
        alert('hi,', this.name)
    }
}

function Dog(name, age) {
    this.name = name;
    this.age = age;
    this.method = function() {
        alert('wolf wolf', this.name)
    }
}
var obj1 = new Person('david', 18);     // obj1叫做构造函数Person()的实例
console.log(obj1);

var dog1 = new Dog('korea', 3);         // dog1叫做构造函数Dog()的实例
console.log(dog1);
```
<img width="513" alt="截屏2020-02-03下午3 07 13" src="https://user-images.githubusercontent.com/26485327/73632510-dde48080-4696-11ea-9a23-1eec05d0a7af.png">

- 与最开始相比，普通函数中需要自行定义一个对象`var obj = new Object()`，并且在手动设定函数返回此对象`return obj`
    ```javascript
    function dog(name) {
        var obj = new Object();     
        obj.name = name;
        return obj;
    }
    ```
- 使用构造函数，由于默认自动创建一个对象，所以函数内部无需手动创建一个对象以及手动返回一个对象
- 图中可以看出，虽然proto都是Object，但是构造函数显示对象的前面，显示了构造函数名Person和Dog
- **使用同一个构造函数创建的对象，叫做一类对象，也可以将一个构造函数称作类**
- 通过一个构造函数创建的对象，称作该构造函数的实例，也称作该类的实例。使用`instanceof`函数来判断**一个对象是否为一个构造函数的实例**
    - `console.log(obj1 instanceof Person);     // true`    
    - `console.log(obj1 instanceof Object);     // true`，所有对象都是Objec的后代

- `this.name = name; `，表示把传入的name值，赋值给新建的那个对象的name属性

### 改进
可以看到上面用于创建对象的构造函数中，写以一个方法函数。因此没调用一次构建函数来创建一个新的对象，都要创建一个新的方法函数。而函数的功能是完全一样的，这样就会在堆内存中开辟很多个同样功能的函数。可以将该方法函数，放在全局作用域中，来让构造函数中的方法去调用，来实现同样功能的函数只创建一次，来节省内存
```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.method = methodfun
}

function methodfun() {
    alert('hi,', this.name)
}
```

但是将构造函数中的方法函数放到全局作用域后，会污染全局作用域的命名空间，其他人不能再次使用该函数名，如果别人使用了，则会覆盖掉你创建个的函数。因此这么方法并不好。

更好的方法是将，共同拥有的方法函数，或者是变量，放到构建函数的原型对象中



# 3. 原型对象prototype
- 我们创建的任何一个函数，解析器（浏览器）都会向函数中添加一个隐藏属性，该隐藏属性对应着一个对象，即为原型对象prototype
- 当函数作为普通函数时，调用prototype没有任何作用
- 当函数作为构造函数时，通过该构造函数创建的所有对象，都会包含一个隐含属性，也即为构造函数的原型对象属性prototype
    - 在构造函数中，通过prototype来调用
    - 在构造函数创建的对象中，通过__proto__来调用
- 原型对象就相当于一个公共空间，同一个构造函数创建的对象，都可以访问。因此可以将一组对象中共有的内容，放到原型对象中


<img width="513" src="https://user-images.githubusercontent.com/26485327/73637492-679a4b00-46a3-11ea-867a-6f90083a4c2f.png">

```javascript
function MyClass() {

}

MyClass.prototype.a = 123;          // 函数也是一种对象，可以直接 对象名.属性 来添加
console.log(MyClass.prototype);

var mc = new MyClass();
console.log(mc.__proto__);
```


在对象中调用一个属性或者方法时，首先在对象内部寻找，有则直接调用，没有则去原型对象中查找

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
    // this.method = methodfun;
}

Person.prototype.method = function() {
    console.log('hello!!', this.name);
}

var obj1 = new Person('david', 18);
console.log(obj1);
obj1.method();
```
<img width="453" alt="截屏2020-02-03下午5 07 17" src="https://user-images.githubusercontent.com/26485327/73639580-a4684100-46a7-11ea-89d9-8612a9ba7540.png">

- 图片中可以看到，obj1对象中并没有方法函数，但下面依然可以调用成功，就是在原型对象中找到的

## 原型对象的原型

```javascript
function MyClass() {

}

MyClass.prototype.a = 123;

var mc = new MyClass();
console.log(mc);

console.log('a' in mc);                                                 // true
console.log(mc.hasOwnProperty('a'));                                    // false
console.log(mc.hasOwnProperty('hasOwnProperty'));                       // flase
console.log(mc.__proto__.hasOwnProperty('hasOwnProperty'));             // flase
console.log(mc.__proto__.__proto__.hasOwnProperty('hasOwnProperty'));   // true
console.log(mc.__proto__.__proto__.__proto__);                          // null
```
<img width="557" alt="截屏2020-02-03下午6 04 37" src="https://user-images.githubusercontent.com/26485327/73644083-a6360280-46af-11ea-8da2-02d2d7b6333b.png">


- `对象属性 in 对象`，可以判断一个对象是否含有一个属性或者方法函数，但是此处可以看到，a属性并没有在对象中定义，依然返回true，就是从原型对象中找到了a这个属性
- `对象.hasOwnProperty('属性')`，仅判断一个属性是否存在于对象中，不出查找原型对象
- 那么从上面看得出来`hasOwnProperty`本身，又是哪里来的？反正我没有去定义这个一个方法函数，因此我们去对象的原型中找找
- `对象.__proto__.hasOwnProperty('hasOwnProperty')`，对象的原型中，依然没有找到hasOwnProperty这个方法函数，接下来去对象原型的原型中去找找
- `对象.__proto__.__proto__.hasOwnProperty('hasOwnProperty')`，诶！找到了
- 原型还有其自己的原型，再往下就到头了，没有第三层的原型了
    - 直到找到Object的原型为止，Object的原型没有原型

<img width="506" alt="截屏2020-02-03下午6 01 38" src="https://user-images.githubusercontent.com/26485327/73643857-3b84c700-46af-11ea-90de-3530d5815add.png">

## 对象的toString()方法

- 当通过构建函数创建了一个对象实例后，`console.log(对象实例)`打印出的结果和`对象实例.toString()`的结果是一样的
- 而toString这个方法是构造函数原型的原型里面的函数，弱项修改打印的输出值，可以在构造函数中主动创建一个toString函数

```
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.toString = function() {
    return "[name = " + this.name + ", age = " + this.age + "]"
}

var obj = new Person('david', 22);
console.log(obj);               // Person {name: "david", age: 22}
console.log(obj.toString());    // [name = david, age = 22]
```
<img width="433" alt="截屏2020-02-03下午9 08 55" src="https://user-images.githubusercontent.com/26485327/73655627-654ae780-46c9-11ea-9692-f6ad2b050b18.png">
- 由于是chrome，所以直接打印obj和obj.toString不一样，是因为chrome做了优化


# 4. 辣鸡回收Garbage Collection

<img width="761" src="https://user-images.githubusercontent.com/26485327/73656778-cc699b80-46cb-11ea-8562-f2ab16cfe525.png">

- 当一个对象，没有被任何变量或是属性引用时，此时，将永远无法操作此对象，即为垃圾。占用大量内存空间

- js有自动垃圾回收机制，解析器（浏览器）会自动将没有用的程序代码清理掉，而无需手动删除
- 需要手动操作的是，将没用的对象设置为null，浏览器就会自动进行辣鸡清理







