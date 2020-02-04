数组去重？？？

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
### 3.1 for循环遍历
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

### 3.2 数组forEach()方法遍历 - IE8不支持
- 数组的foreach方法需要一个函数作为参数
  - 这种函数有我们创建，但不由我们调用，由浏览器调用，称为回调函数

- 数组中有几个元素，该回调函数就会被执行几次，没执行一次，浏览器就会遍历到数组中的一个元素
  - 浏览器遍历到的元素将以实参的形式传递给回调函数，我们可以通过形参来读取这些内容
- 浏览器会在回调函数中传递三个参数
    1. 数组的元素的值value
    2. 数组的元素的索引index
    3. 正在遍历的数组本身
- 若考使用IE8，则不能使用该方法
- 手机端开发可以大胆使用

```javascript
arr.forEach(function(value, index, obj) {
    console.log('value: ', value);
    console.log('index: ', index);
    console.log('obj: ', obj);
    console.log('\n');
})
```
<img width="424" alt="截屏2020-02-04下午1 17 06" src="https://user-images.githubusercontent.com/26485327/73715972-a76b3c00-4750-11ea-8c2f-555dddf4da48.png">


# 4. slice & splice
### slice
- 通过索引，从数组中提取出指定元素，不会改变原数组，将选取的元素封装到一个新数组
- 索引`[start, end)`，包含开始索引，不包含结束索引
  - 不指定结束索引，表示一直到数组左后一个元素
  - 负数索引为末尾开始的索引

### splice
- 通过索引，将指定元素从原数组中删除，会改变原有数组，并向数组中添加一个或多个新元素
- 被删除的元素会作为返回值返回
- 索引`(开始索引，删除数量，新元素)`，注意第二个参数为从开始索引往后删除的元素的个数，而不是结束索引
  - `arr.splice(1,0)`，表示从索引1开始删除0个元素，就是一个都不删

# 5. concat()
- 拼接一个或多个喝数组，返回拼接后的新数组，不会影响原数组
- `res = arr1.concat(arr2, arr2, 'a','b')`，可以拼接数组，也可以拼接元素

# 6. join（）
- 将数组转换为一个字符串，返回的字符串通过逗号连接，不影响原数组
- `res = arr.join()`，把数组中的元素，拼接为一个字符串
- 默认通过逗号将数组中的元素拼接，可以指定拼接用的符号，不要符号可以使用空字符串`''`来拼接
  - `res = arr.join('')`

# 7. reverse（）
- 前后颠倒元素前后顺序

# 8. sort（）
- 按照unicode编码排序
- 会影响原数组
- 当排序数字的时候，默认会出现问题
```javascript
arr = [1, 4, 7, 2, 3, 22, 11];
arr.sort();
console.log(res);   // (7) [1, 11, 2, 22, 3, 4, 7]
```
- 准确按照数字大小排序，需要在sort函数中添加一个回调函数，来自行指定排序规则
  - 回调函数中定义两个形参
  - 浏览器会分别依次使用数组中的元素，作为实参，去调用回调函数
  - 浏览器根据回调函数的返回值决定元素顺序
    - 返回大于0的值，则交换元素为止
    - 返回值小于0，则不交换元素位置
    - 返回0，认为元素相等，也不交换元素位置
    
```javascript
arr = [1, 4, 7, 2, 3, 22, 11];

arr.sort(function(a, b) {
    if (a > b) {
        return 1;
    } else {
        return -1;
    }
});
console.log(arr);
```
<img width="309" alt="截屏2020-02-04下午3 24 06" src="https://user-images.githubusercontent.com/26485327/73722831-6419c900-4762-11ea-9a2e-a44fe3dad22c.png">




















