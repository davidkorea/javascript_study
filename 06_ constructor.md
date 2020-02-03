# 构造函数（~类）

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
- 那如果我想让他们不显示Object，二十显示自定义的person或是dog呢？

使用构造函数即可，类似于python的class
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

1. new关键字会自动在堆内存中开辟一块空间，换句话说就是自动创建一个对象
    - `var obj = new Person();`，obj就是自动被创建的对象
2. 将自动创建的对象设置为函数的this，也就是说，在构造函数中可以通过this来引用新创建的对象
    - `alert(this);`，其中this代指上面自动创建的obj对象
3. 逐行执行函数代码
4. 将这个自动创建的对象作为返回值返回

```javascript
function Person(name, age) {
    this.name = name;
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
var obj1 = new Person('david', 18);
console.log(obj1);

var dog1 = new Dog('korea', 3);
console.log(dog1);
```
<img width="513" alt="截屏2020-02-03下午3 07 13" src="https://user-images.githubusercontent.com/26485327/73632510-dde48080-4696-11ea-9a23-1eec05d0a7af.png">

- 与最开始相比，普通函数中需要自行定义一个对象，并且在手动设定函数返回此对象
- 使用构造函数，由于默认自动创建一个对象，所以函数内部无需手动创建一个对象以及手动返回一个对象
- 图中可以看出，虽然proto都是Object，但是构造函数显示对象的前面，显示了构造函数名Person和Dog

















