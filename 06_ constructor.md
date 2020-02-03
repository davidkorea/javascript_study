# 构造函数（类）

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
- 构造函数调用时需要使用关键字new
- 构造函数创建事，函数名首字母默认大写





















