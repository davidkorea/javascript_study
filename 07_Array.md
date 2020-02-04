# 1. 数组Array Basics

对象分为：内建对象，宿主对象，自定义对象。之前04，05，06都是讲解的自建对象，即创建一个自定义对象。

Array是一个内建对象，是ES标准中实现的。
- 相较于自定义一个对象，Array的效率要更高，性能更好，一般情况下还是使用数组存储数据
- 自定义对象是通过属性名来访问属性值
  ```
  var obj = new Object();
  obj.name = 'david';
  
  obj.name;      // 取得属性的值 
  ```
- Array数组是通过索引（0，1，2...）来取得元素的值
  ```
  var arr = new Array();
  arr[0] = 'david';
  
  arr[0];      // 取得元素的值
  ```
- **连续**数组的长度，使用length属性来查看，`数组.length`，不连续数组不可以使用
  ```javascript
  var arr = new Array();
  arr[0] = 0;
  arr[1] = 1;
  arr[100] = 100;

  console.log(arr);
  console.log(arr.length);
  ```
  <img width="393" alt="截屏2020-02-03下午9 58 50" src="https://user-images.githubusercontent.com/26485327/73659028-5f0c3980-46d0-11ea-8594-1d910835860c.png">

  - 连续数组每次都向数组最后添加新元素
    ```javascript
    var arr = new Array();
    arr[0] = 0;
    arr[1] = 1;
    arr[arr.length] = 100;

    console.log(arr);
    console.log(arr.length);
    ```
    <img width="372"  src="https://user-images.githubusercontent.com/26485327/73659382-1bfe9600-46d1-11ea-8ddd-dd2dc9575ca1.png">

- 创建一个数组
  - `var arr = [1,2,3,4]`，更简单，更灵活
  - `var arr = new Array(1, 2, 3);`
  - 定义空数组长度，但是用的不多，虽然定义长度，使用时可以超过此长度
    ```
    arr1 = new Array(3);
    console.log(arr1);
    ```
    <img width="320" src="https://user-images.githubusercontent.com/26485327/73660517-4c473400-46d3-11ea-8093-494a411cb7c6.png">


# 2. 数组的常用方法
#### push（）
数组的最后添加一个或多个元素，并返回数组的新的长度

#### pop（）
删除数组最后一个元素，并返回被删除的元素

#### unshift（）
数组的开头添加一个或多个元素，并返回数组的新的长度

#### shift（）
删除数组的第一个元素，并返回被删除的元素


# 3. 遍历数组
```javascript
for (i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
```

创建几个Person对象，放到一个数组，再将这个数组中对象年龄大于20的找出来，放到一个新的数组中
```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.toString = function() {
    return " {name = " + this.name + ", age = " + this.age + "}"
}           // 必须要有定义这个方法，否则chrome的log里面可以被优化显示，而到网页中无法显示

var per1 = new Person('david', 22);
var per2 = new Person('korea', 19);
var per3 = new Person('china', 23);
var per4 = new Person('jinan', 26);
var arr = [per1, per2, per3, per4];

function bigger20(arr) {
    var newArr = [];
    for (i = 0; i < arr.length; i++) {
        if (arr[i].age > 20) {
            newArr.push(arr[i]);
        }
    }
    return newArr
}

var res = bigger20(arr);
document.write(res);
```
<img width="379" alt="截屏2020-02-03下午11 44 38" src="https://user-images.githubusercontent.com/26485327/73667380-258efa80-46df-11ea-8adc-958f3a83f893.png">
<img width="604" alt="截屏2020-02-03下午11 44 11" src="https://user-images.githubusercontent.com/26485327/73667343-16a84800-46df-11ea-9c9a-01fcf9fc4b29.png">

### forEach（）
- 数组的foreach方法需要一个函数作为参数
  - 这种函数有我们创建，但不由我们调用，由浏览器调用，称为回调函数

- 数组中有几个元素，该回调函数就会被执行几次，没执行一次，浏览器就会遍历到数组中的一个元素
  - 浏览器遍历到的元素将以实参的形式传递给回调函数，我们可以通过形参来读取这些内容
- 浏览器会在回调函数中传递三个参数
    1. 数组的元素的值value
    2. 数组的元素的索引index
    3. 正在遍历的数组本身


