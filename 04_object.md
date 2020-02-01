数据类型
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

对象的分类
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











