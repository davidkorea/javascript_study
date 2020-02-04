

# 包装类

将简单数据类型转换成对象

- numbver -> Number()
- string -> String()
- boolean -> Boolean

```javascvript
var str = new String('hello');
var num = new Number(2);
var bool = new Boolean(true);

console.log(typeof str);
console.log(typeof num);
console.log(typeof bool);
```
<img width="188" alt="截屏2020-02-04下午8 39 04" src="https://user-images.githubusercontent.com/26485327/73745608-642fbe00-478e-11ea-87ad-fa7f1d084d1e.png">

但是使用基本数据类型对象时，会出现问题
```javascript
var num1 = new Number(2);
var num2 = new Number(2);

console.log(num1 == num2);    // flase
```
- 同样的数字，比较确是flase
- 比较两个对象是否一样，实际上是比较的对象的内存地址
- 基本类型转换做对象使用，不方便

既然不好用，那么包装类的使用场景是？
```javascript

var a = 123;
a = a.toString();

console.log(a);             // 123
console.log(typeof a);      // string
```
- 只有对象数据类型才有属性和方法，因此上面定义的a变量应该是没有.String()方法的
- 那么根据输出结果看得出，实际上这个基本变量类型已经从num转换成的string
- 原理就是浏览器临时使用包装类将简单类型转换为对象，在后在调用对象的方法
- 调用完成以后，再将其转换为基本数据类型

**简单说就是，包装类是浏览器自己来使用的，开发时不这么用**

下面说一下，常用的String()包装类，注意也是浏览器用，而不是我们自定去创建一个String()对象

# String()对象












