#### 一个域名地址的组成
  http://　　www  　.　　abc.com　　:8080  　/　　　script/jquery.js  
  协议　　 子域名　　　　主域名　　　端口号　　　　　　请求资源地址　　
  
  ##### 当协议、子域名、主域名、端口号任意一个不相同时，都算作不同域
  ##### 不同域之间相互请求资源，就算作跨域
#### 跨域方法
    ##### 主域和子域
        ###### www.a.com 和 child.a.com
        ###### 主域和子域都设置：document.domain="a.com"
            \- https://developer.mozilla.org/zh-CN/docs/Web/Security/Same-origin_policy
    ##### 服务器代理
    ##### JSONP
        ###### 利用script标签，将其src当做请求地址，只要地址返回的是json或js，
        ###### 步骤：
            \- 创建script标签，src指向请求地址，在创建的script标签前声明函数fn：function fn(json){ alert(json) }  
            \- 请求地址返回fn({data:"返回的数据"})
        ###### 限制：只能用作get请求
        
            ```
            function jsonp(url,data,callbackName,dataCallback){
                var timestamp=new Data().getTime();
                var script=document.createElement("script");
                script.id="jsonp"+timestamp;
                url+="?callback"+callbackName;
                for(var key in data){
                    url+="&"+key+"="+data[key];
                }
                script.src=url;
                document.getElementsByTagName("body")[0].appendChild(script);
                window[callbackName]=function (json){
                    return JSON.parse(json);                
                }
                var data=window[callback]();
                document.getElementsByTagName("body")[0].removeChild(script);
                dataCallback.bind(window,data);
            }
            jsonp("www.baidu.com",{},"getData",function(data){
                
            })
            ```
    ##### 利用location.hash和iframe：
    ##### 利用window.name和iframe
        
    ##### XHR2
        \- H5提供的XMLHttpRequest Level2已经实现了跨域
        在服务端设置如下头部信息即可：  
        　header('Access-Control-Allow-Origin: * ');  
        　header('Access-Control-Allow-Methods: POST,GET ');  
        \- 兼容性：IE10+  
        \- 低版本IE可使用XDomainRequest对象实现跨域，用法同XMLHttpRequest 
    ##### window.postMessage()


参考：  
　https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS  
　http://bbs.miaov.com/forum.php?mod=viewthread&tid=5551  
　http://tingandpeng.com/2016/09/05/%E5%89%8D%E7%AB%AF%E8%B7%A8%E5%9F%9F%E8%AF%B7%E6%B1%82%E5%8E%9F%E7%90%86%E5%8F%8A%E5%AE%9E%E8%B7%B5/