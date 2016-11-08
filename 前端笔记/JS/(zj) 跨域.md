## 一个域名地址的组成
  http://　　www  　.　　abc.com　　:8080  　/　　　script/jquery.js  
  协议　　 子域名　　　　主域名　　　端口号　　　　　　请求资源地址　　

**当协议、子域名、主域名、端口号任意一个不相同时，都算作不同域**  
**不同域之间相互请求资源，就算作跨域**  
## 跨域方法
### 1. 主域和子域或不同子域间
\- www.a.com 和 child.a.com  
\- 主域和子域都设置：document.domain="a.com"  
\- https://developer.mozilla.org/zh-CN/docs/Web/Security/Same-origin_policy
### 2. 服务器代理
### 3. JSONP
\- 利用script标签，将其src当做请求地址，只要地址返回的是json或js  
**步骤**：  
\- 创建script标签，src指向请求地址，在创建的script标签前声明函数fn：function fn(json){ alert(json) }  
\- 请求地址返回fn({data:"返回的数据"})  
**限制**：  
\- 只能用作get请求

```js
function jsonp(url,data,callbackName,dataCallback){
    // 时间戳
    var timestamp=new Date().getTime();
    // 创建script元素
    var script=document.createElement("script");
    // 设置id
    script.id="jsonp"+timestamp;
    url+="?callback="+callbackName;
    for(var key in data){
        url+="&"+key+"="+data[key];
    }
    //通过jsonp取得的数据（默认范围的格式为json字符串）
    var data;
    window[callbackName]=function (json){
      data = JSON.parse(json);                
    }
    script.src=url;
    //插入script元素
    document.getElementsByTagName("body")[0].appendChild(script);
    dataCallback.bind(window,data);
    //删除script元素
    document.getElementsByTagName("body")[0].removeChild(script);
    data=null;
}

jsonp("https://www.baidu.com",{},"getData",function(data){
  //取得数据后的回调
})
```
### 4. 利用location.hash和iframe：
\- 详见《前端跨域整理   Damonare的个人博客.png》
### 5. 利用window.name和iframe

### 6. XHR2
\- H5提供的XMLHttpRequest Level2已经实现了跨域
在服务端设置如下头部信息即可：  
　header('Access-Control-Allow-Origin: * ');  
　header('Access-Control-Allow-Methods: POST,GET ');  
\- 兼容性：IE10+  
\- 低版本IE可使用XDomainRequest对象实现跨域，用法同XMLHttpRequest
### 7. window.postMessage()
\- 详见《 H5跨文档消息通信（妙味）》  
\- 详见《前端跨域整理   Damonare的个人博客.png》

**参考**：  
- https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS  
- http://bbs.miaov.com/forum.php?mod=viewthread&tid=5551  
- http://tingandpeng.com/2016/09/05/%E5%89%8D%E7%AB%AF%E8%B7%A8%E5%9F%9F%E8%AF%B7%E6%B1%82%E5%8E%9F%E7%90%86%E5%8F%8A%E5%AE%9E%E8%B7%B5/  
- http://damonare.github.io/2016/10/30/%E5%89%8D%E7%AB%AF%E8%B7%A8%E5%9F%9F%E6%95%B4%E7%90%86/#more  
- http://www.cnblogs.com/2050/p/3191744.html  
- 《前端跨域整理   Damonare的个人博客.png》
