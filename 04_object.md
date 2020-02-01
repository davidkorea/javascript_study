### 数据类型
- string
- number
- boolean
- null
- undefined
- **object**

举例说明
当描述一个人的信息时，姓名，性别，年龄，可以使用单一类型变量表示，但是相互没有联系，一个年龄的数字和一个姓名对应的不一定是同一个人
```javascript
var name = 'david';
var gender = 'male';
var age = 18;
```
- 可以理解为，超市的货架上有很多商品，但不能说明那些属于你
- 把几个商品放在你自己的**塑料袋**里，那么这些商品就是你的
- 此处，将多个变量保存在同一个对象中，也即，一个对象可以有多种不同变量类型

### 对象的分类
1. 内建对象
    - ES标准中定义的对象，任何ES的实现中都可以直接使用，如浏览器，node.js
    - Math，String，Number等等
2. 宿主对象
    - 由运行环境提供的对象，目前主要指浏览器提供的对象
    - BOM中的console.log()，DOM中的ducoment.write()
3. 自建对象，自定义对象
    - 自行定义
    - 定义一个塑料袋，在往里装东西
    ```javascript
    var obj = new Object();

    obj.name = 'david';
    obj.gender = 'male';
    obj.age = 18;

    console.log(obj);
    // {name: "david", gender: "male", age: 18}

    obj.age = 22;
    delete obj.gender;
    ```
    - 使用new关键字调用的函数，叫做构造函数constructor，构造函数是专门用于创建对象的函数
        - `var obj = new Object();`
    - 对象中保存的值，称作属性
        - `对象.属性名 = 属性值;`
    - 读取对象中的属性
        - `对象.属性名;`
        - 读取对象中没有的属性，不报错，返回undefined
    - 修改属性值
        - `对象.属性名 = 新属性值;`
    - 删除对象的属性
        - `delete 对象.属性名;`


# 对象名和对象的值
### 属性名
1. `对象名.属性名 = 属性值`
2. `对象名["属性名"] = 属性值`，此种方式更加灵活，已经传入变量来当作属性名，即中括号可以传递变量
    ```javascript
    var obj = new Object();
    obj['nihao'] = 'hello';

    var i = 'nihao';
    console.log(obj[i]);   
    // hello
    ```
### 属性值
1. 属性值可以是任何单一数据类型
2. 属性值也可以是一个对象
    ```javascript
    var obj = new Object();
    obj.name = 'david';
    obj.gender = 'male';
    obj.age = 18;

    var obj2 = new Object();
    obj2.name = 'korea';
    obj2.age = 22;

    obj.text = obj2;        // 对象的属性值可以是一个对象
    console.log(obj);
    
    // {name: "david", gender: "male", age: 18, text: {…}}
    ```
    <img width="419" alt="截屏2020-02-01下午10 01 05" src="https://user-images.githubusercontent.com/26485327/73593353-5a178080-453e-11ea-9586-067e3a8301a6.png">

3. 检查一个属性是在包含于一个对象中
    ```javascript
    console.log('text' in obj);
    // true
    ```






