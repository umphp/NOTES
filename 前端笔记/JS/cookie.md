## 概述
使用 `document.cookie` 属性来创建 、读取、及删除 cookie。  
匹配到当前域名（domain）和路径（path）的未过期cookie会附加到当前页面的所有请求的请求头中。

**注意**：`AJAX（XHR2）`可通过设置`xhr.withCredentials = true`以及服务器端配合设置`header("Access-Control-Allow-Credentials: true")`来支持跨域发送cookies

### 屏蔽请求中携带cookie
- 将静态资源放在不同域或子域下
- ajax请求路径在不同域或子域下

### 安全
**路径限制并不能阻止从其他路径访问cookie**。使用简单的DOM即可轻易地绕过限制(比如创建一个指向限制路径的, 隐藏的iframe, 然后访问其 contentDocument.cookie 属性). 保护cookie不被非法访问的唯一方法是将它放在另一个域名/子域名之下, 利用同源策略保护其不被读取

## 获取cookie
`document.cookie` 将以字符串的方式返回所有的 cookie 。格式如下：
```
cookie1=value; cookie2=value; cookie3=value;`
```

**获取指定的cookie值**：
```js
function getCookie(name){
    var cookies = document.cookie;
    var cookieName = encodeURIComponent(name) + '=';
    var cookieStart = document.cookie.indexOf(cookieName);
    var cookieValue = null;
    if (cookieStart > -1) {
        var cookieEnd = cookies.indexOf(';', cookieStart);
        if (cookieEnd == -1) {
            cookieEnd = cookies.length;
        }
        cookieValue = decodeURIComponent(cookies.substring(cookieStart + cookieName.length, cookieEnd));
    }
    return cookieValue;
}

// 通过正则获取cookie
function getCookie(name) {
    // (^| ) 以后面的字符或空格开始。
    // ([^;]*) 只匹配除了;号之外的所有字符。
    // (;|$) 匹配以;号或以前面的字符为结尾的字符。
    if (name && new RegExp("(^| )" + name + "=([^;]*)(;|$)").exec(document.cookie)){
        return decodeURIComponent(RegExp.$2);
    } 
}

```
## 新建或修改cookie
通过`document.cookie`重新赋值新建或修改cookie（并不会完全重写cookie，相当于添加操作）。  

**新建或修改cookie**：
```
document.cookie="name=paul";
```
### 可配置参数

**expires**：    
为 cookie 添加一个过期时间（以 UTC 或 GMT 时间）。默认情况下，cookie 在浏览器关闭时删除
```
document.cookie="name=paul; expires=Thu, 18 Dec 2013 12:00:00 GMT";
```
**max-age**：  
设置cookie的有效时长。单位：秒
```
// 设置cookie有效期一年
document.cookie="name=paul; max-age=365*24*60*60";
```

**path**：  
设置cookie的路径。默认情况下，cookie 属于当前页面。
```
// 设置cookie属于根路径
document.cookie="name=paul; expires=Thu, 18 Dec 2013 12:00:00 GMT; path=/";
```
**domain**：
设置cookie的域名。默认为当前文档位置的路径的域名部分。
```
// 设置域名为 "*.a.com"
document.cookie="name=paul; expires=Thu, 18 Dec 2013 12:00:00 GMT; path=/;domain=.a.com";
```
**secure**：
设置cookie是否只通过https协议传输
```
document.cookie="name=paul; expires=Thu, 18 Dec 2013 12:00:00 GMT; path=/;domain=.a.com;secure";
```


**设置或修改指定cookie**
```js
function setCookie(opts) {
    var name = opts.name;
    var value = opts.value;
    var expires = opts.expires; // 
    var path = opts.path;
    var domain = opts.domain;
    var secure = opts.secure;
    var cookieText = encodeURIComponent(name) + '=' + encodeURIComponent(value);
    if (expires) {
        switch (expires.constructor) {
        case Number: // 单位秒
          cookieText = expires === Infinity ? "; expires=Fri, 31 Dec 9999 23:59:59 GMT" : "; max-age=" + expires;
          break;
        case String:
          cookieText = "; expires=" + expires;
          break;
        case Date:
          cookieText = "; expires=" + expires.toUTCString(); // 或者 toGMTString()
          break;
        }
    }
    if (path) {
        cookieText += '; path=' + path;
    }
    if (domain) {
        cookieText += '; domain=' + domain;
    }
    if (secure) {
        cookieText += '; secure';
    }
    document.cookie = cookieText;
}
```

## 删除cookie
设置 expires 参数为以前的时间即可
```
document.cookie = "name=; expires=Thu, 01 Jan 1970 00:00:00 GMT";
```
**注意**：
- 删除时不必指定 cookie 的值
- 如果要删除非当前路径下的cookie，需制定`path`参数

**删除指定cookie**
```js
function removeCookie(name) {
    document.cookie = name + "= ; expires=" + new Date(0);
}
```
**清楚所有cookie**
```js
function clearCookie(path,domain){
    // 获取所有cookie的key
    var keys = document.cookie.match(/(?!\s)([^;\=]+)(?=\=.*(;|$))/g);
    var forPath = path ? ";path=" + path : "";
    forPath += domain ? ";domain=" + domain : "";
    keys.forEach(function(item,index){
        document.cookie = item + "= ; expires=" + new Date(0) + forPath;
    });
}
```


**参考**：
- http://www.runoob.com/js/js-cookies.html
- https://developer.mozilla.org/zh-CN/docs/Web/API/Document/cookie