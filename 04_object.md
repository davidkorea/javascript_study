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
- 把几个商品放在你自己的包里，那么这些商品就是你的
- 此处，将多个变量保存在同一个对象中，也即，一个对象可以有多种不同变量类型

对象的分类
1. 内建对象
    - ES标准中定义的对象，任何ES的实现中都可以直接使用，如浏览器，node.js
    - Math，String，Number等等
2. 宿主对象
    - 由运行环境提供的对象，目前主要指浏览器提供的对象
    - BOM中的console.log()，DOM中的ducoment.write()
3. 自建对象，自定义对象

