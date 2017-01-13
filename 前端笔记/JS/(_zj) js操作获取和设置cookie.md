
```

//创建cookie
function setCookie(opts) {
    var name=opts.name;
    var value=opts.value;
    var exdays=opts.exdays;
    var path=opts.path;
    var domain=opts.domain;
    var secure=opts.secure;
    var cookieText = encodeURIComponent(name) + '=' + encodeURIComponent(value);
    if (expires) {
        var d = new Date();
        d.setTime(d.getTime()+(exdays*24*60*60*1000));
        cookieText += '; expires=' + d.toGMTString();
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

//获取cookie
function getCookie(name) {
    var cookieName = encodeURIComponent(name) + '=';
    var cookieStart = document.cookie.indexOf(cookieName);
    var cookieValue = null;
    if (cookieStart > -1) {
        var cookieEnd = document.cookie.indexOf(';', cookieStart);
        if (cookieEnd == -1) {
            cookieEnd = document.cookie.length;
        }
        cookieValue = decodeURIComponent(document.cookie.substring(cookieStart + cookieName.length, cookieEnd));
    }
    return cookieValue;
}

// 通过正则获取cookie
function getCookie(name) {
    // (^| ) 以后面的字符或空格开始。
    // ([^;]*) 只匹配除了;号之外的所有字符。
    // (;|$) 匹配以;号或以前面的字符为结尾的字符。
    if (name && RegExp("(^| )" + name + "=([^;]*)(;|$)").exec(document.cookie)) return RegExp.$2;
}

//删除cookie
function unsetCookie(name) {
    document.cookie = name + "= ; expires=" + new Date(0);
}

```
