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
  
  if (/chrome/i.test(userAgent)) {
      alert('chrome');
  } else if (/safari/i.test(userAgent)) {
      alert('safari');
  } else {
      alert('???');
  }
  ```
  
  
  
  
  
  
  
  
  
