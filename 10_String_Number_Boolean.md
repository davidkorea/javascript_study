
- **字符串可以使用负索引**，但是数组Array不可以使用负索引！！

-----

# 包装类

将简单数据类型转换成对象

- numbver -> Number()
- string -> String()
- boolean -> Boolean

```javascript
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

- 字符串在底层是以字符数组的形式保存
  `var str = 'hello';` -> `['h','e','l','l','o']`

**字符串的属性**
- 字符串有长度 str.length
- 字符串可以被索引 str[2]
  

**字符串的方法**
- str.charAt(索引)，字符串中指定位置的字符，与使用中括号[]实现的功能相同
- str.charCodeAt(索引)，对应指定字符的unicode
- String.fromCharCode(字符编码)，将unicode编码转换为字符
  - `String.fromCharCode(0x2692)` -> ⚒
- str.concat()，连接2个或多个字符串，和加号+的功能相同
- str.indexOf(字符, 开始查找位置的索引)，检索字符串中是否包含该字符，有则返回对应第一次出现索引，没有找到则返回-1
  - `str.indexOf('l')` -> 2，l在hello的第2索引第一次出现的位置
  - `(str.indexOf('l', 3)` -> 3，从字符串hello的第三个索引为止开始索引，那么l则可以呗检索到，返回对应索引3
- str.lastIndexOf()，用法和indexOf一样，但是从后往前检索
- str.slice(1,-1)，可以使用负数索引，倒数
- str.substring(1，3)，和slice功能一致，但是不能接收负数索引，如果第二个参数小于第一个参数，会自动调整参数顺序
- str.split('')，将字符串分割成字符，'hello' ->  ["h", "e", "l", "l", "o"]，也可以自定义拆分符
- str.toUpperCase(), str.toLowerCase()



