# Date

Date和Array一样，也是内建对象

- 使用构造函数创建一个Date对象，那么输出为当前代码执行的时间
```javascript
var d = new Date();
console.log(d);   // Tue Feb 04 2020 17:41:48 GMT+0800 (中国标准时间)
```

- 也可以指定一个固定的时间
```javascript
var d = new Date("2020-02-02"");
console.log(d);   // Sun Feb 02 2020 08:00:00 GMT+0800 (中国标准时间)
```

Date对象的一些方法

1. getDate(），当前日期的几号/几日
2. getDay(), 星期几，返回0-6，0代表周日，其他代表周一至周六
3. getMonth()，月份，0表示一月，11表示十二月
4. getFullYear()，年份
5. gettime()，时间戳，一串数字1580601600000，格林威治标准时间1970年1月1日 0时0分0秒，到当前所花费的毫秒数
    - 由于年月， 时分秒， 毫秒的进制不同，为了计算机处理方便，同意用毫秒计数
    ```javascript
    var d = new Date("1970-01-01 00:00:00");
    console.log(d);
    console.log(d.getTime());     // -28800000,东八区中国时间，早于格林威治8小时
    ```
    <img width="402" alt="截屏2020-02-04下午6 00 13" src="https://user-images.githubusercontent.com/26485327/73734192-33448e80-4778-11ea-8f37-da16d48b5cae.png">
6. now()，Date.now()，执行当先代码的时间戳
