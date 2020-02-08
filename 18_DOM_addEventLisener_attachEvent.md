
# addEventLisener & attachEvent

同时为一个元素的**同一个事件**添加多个响应函数

- 使用`元素.onclick = function(){}`的方式，下面的对覆盖掉前面的函数，因此只会执行对后面一个响应函数
- 适用`元素.addEventLisener("click", function(){}, false)`，三个参数，但是后面的addEventLisener不会覆盖掉前面的addEventLisener，而是所有的addEventLisener都会依次执行
  - addEventLisener中的this，代指调用addEventLisener的元素
- IE8及以下不支持addEventLisener，可以使用`attachEvent('onclick', function(){})`，两个参数，执行顺序为从后往前
  - attachEvent中的this，代指window
  
兼容所有浏览器
- 统一this

