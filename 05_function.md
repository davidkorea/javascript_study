
- 函数也是一个对象
- 对象object是将一组属性放在一个塑料袋
  - `var obj = new Object();`
- 函数function是将一个功能封装起来，方便其他函数进行调用
  - `var func = new Function();`
  - 对象具有的功能函数也全都具有
  - 但是一般是使用构造函数的方式创建一个函数对象，而是使用函数声明来创建一个函数
    ```javascript
    function 函数名([参数1，参数2...]){
      语句...
    }
    ```
