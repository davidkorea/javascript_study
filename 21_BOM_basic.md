# 浏览器对象模型

BOM提供了一组对象来操作浏览器
- window
  - 整个浏览器窗口，也是网页中的全局对象
- navigator
  - 当前浏览器的信息，识别不同类型浏览器
- location
  - 浏览器当前地址栏信息，或者操作浏览器跳转页面
- history
  - 浏览器历史记录，由于隐私原因，不能获取到具体的历史记录，只能操作浏览器向前向后翻页
  - 只在档次访问时有效
- screen
  - 用户的屏幕（显示器）信息
  - 更多用在移动端
  
  
BOM对象在浏览器中
- 作为window的属性保存，可以window.navigator，window.location
- 也作为全局变量，可以直接调用navigator，location

# 1. navigator

![6550452B-DC67-47EA-9376-363C3B781137](https://user-images.githubusercontent.com/26485327/74097945-1976c300-4b4d-11ea-9b15-1b1c9cfb937f.jpeg)

- 由于历史原因，navigator的大部分属性，不能用来有效确认浏览器信息
- 一般只会使用userAgent，**用户代理等价于浏览器**
  - 不同浏览器有不同userAgent
  - `Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.130 Safari/537.36`
  - `Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.5 Safari/605.1.15`
  ```javascript
  var userAgent = navigator.userAgent;
  
  if (/chrome/i.test(userAgent)) {          // i 忽略大小写
      alert('chrome');
  } else if (/safari/i.test(userAgent)) {
      alert('safari');
  } else {
      alert('???');
  }
  ```
- 如果userAgent不能判断浏览器信息，如IE11，则找到IE11独有的一些对象，如果有就是IE11
  ```javascript
    if (window.ActiveXObject) {       // IE 8,9,10 ok
        alert('IE');
    }
  ```
  - 虽然IE11有这个属性，但是转换成boolean时，时false，微软做了手脚
  ```javascript
  if ('ActiveXObject' in window) {    // IE 11
      alert('IE');
  }
  ```

# 2. history
操作浏览器向前向后翻页，浏览器关闭后，历史记录消失
属性
- length，访问页面的个数
方法
- back，同浏览器后退按钮
- forward，同浏览器前进按钮
- go，跳转到指定界面，需要整数参数
  - go(1)，向前1个页面
  - go(-1)，向后1个页面
  
# 3. location
地址栏
- console.log(location)，当前页面的地址
- `location = www.a.com`，修改location的值，可以实现页面跳转，并生成响应的历史记录history  
  
属性，如图

方法
- assign，和直接给location赋值的效果一样
- reload，重新加载当前页面，和浏览器刷新按钮一样
  - `reload(true)`，强制清空缓存刷新界面，清楚一个输入框里面的信息等
- replace，也可以跳转页面，但是不能后退回去，不生成历史记录
  
# 4. screen

# 5. window
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
