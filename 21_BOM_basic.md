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

