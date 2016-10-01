- ### 参数
    - ####  fn.call ( thisObj,agr1,agr2...)
    - ####  fn.apply ( thisObj, array )
        \- IE9+  
        \- 第二个参数可以为类数组（ES5新增：IE10+）
    - ####  fn.bind ( thisObj,agr1,agr2...)
        \- 返回this值绑定为thisObj的新函数，无论该新函数怎么被调用，this始终绑定为thisObj
- ### Polyfill

```
if (!Function.prototype.bind) {
  Function.prototype.bind = function (oThis) {
    if (typeof this !== "function") {
      // closest thing possible to the ECMAScript 5
      // internal IsCallable function
      throw new TypeError("Function.prototype.bind - what is trying to be bound is not callable");
    }

    var aArgs = Array.prototype.slice.call(arguments, 1), 
        fToBind = this, 
        fNOP = function () {},
        fBound = function () {
          return fToBind.apply(this instanceof fNOP
                                 ? this
                                 : oThis || this,
                               aArgs.concat(Array.prototype.slice.call(arguments)));
        };

    fNOP.prototype = this.prototype;
    fBound.prototype = new fNOP();

    return fBound;
  };
}
```

- ### 相同点
    - #### 如果第一个参数为null或者undefined的话，在非严格模式下，实际上绑定到的是全局对象，这一点对三者都适用。在严格模式下，this值不做转换，即为null或undefined
- ### 一些用法
    - ##### 将类数组转换为数组  
        \- Array.prototype.slice.call(arguments);  
        \- var unboundSlice = Array.prototype.slice;  
         var slice = Function.prototype.call.bind(unboundSlice);  
          slice(arguments); 
    - ##### 获取数组中最大的数值  
        \- Math.max.apply(Math, [1, 2, 3, 5, 7]); 
    - ##### 利用bind实现柯里化
                
        ```
        function fn1(a,b){
            console.log(a,b);
        }
        var fn2=fn1.bind(window,1);
        fn2(); //1 undefined
        ```

**参考**：    
 　　　\- **this**:  https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this  
 　　　\- **bind()**: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind
