# 数组 Array

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



















