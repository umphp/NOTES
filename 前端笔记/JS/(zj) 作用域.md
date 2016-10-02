### 块作用域
    #### with（性能差，不推荐）
    #### try/catch（不推荐）
      \- catch会创建一个块作用域，catch中声明的变量仅在catch中有效
    #### let（ES6）
        ```
        var foo=true;
        if(foo){
            let bar=foo;
            console.log(bar);
        }
        console.log(bar); //ReferenceError
        
        
        for(var i=1;i<=5;i++){
            (function(i){
                setTimeout(function timer(){
                    console.log(i);
                },1000);
            })(i)
        }
        
        for(let i=1;i<=5;i++){
            setTimeout(function timer(){
                console.log(i);
            },1000);
        }
        ```
    #### const（ES6）
        - 用法同let,单const声明的是常量，不能修改，否则报错
### 动态作用域
    #### js不具有动态作用域
    #### 模拟动态作用域
        ##### 利用this（call、apply、bind）
参考：http://www.imooc.com/video/10628