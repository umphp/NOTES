#### 原生

```
//创建XHR对象
var xhr;
if(window.XMLHttpRequest){
    xhr=new XMLHttpRwquest(); //IE7+
}else{
    xhr=new ActiveXObject("Microsoft.XMLHTTP");//IE6
}
//发送请求
xhr.open(method,url,async) 
- method：发送请求方法GET、POST
- async：请求同步false/异步true


xhr.setRequestHeader(key,value) //设置请求头信息

xhr.send(string)
- GET请求时可无参数或为null；POST一般要填参数

//获取服务器响应
xhr.responseText :获取字符串形式的响应数据
xhr.responseXML :获取XML形式的响应数据
xhr.status和xhr.statusText：以数字和文本形式返回HTTP状态码
xhr.getAllResponseHeader() :获取所有的响应报头
xhr.getResponseHeader() :查询响应中的某个字段的值

//监听请求状态
xhr.readyState属性:
0 :请求未初始化,open还没有调用
1 :服务器连接已建立，open已经调用了
2 :请求已接收，也就是接收到头信息了
3 :请求处理中，也就是接收到响应主体了
4 :请求已完成，且响应已就绪，也就是响应完成了

xhr.onreadystatechange事件

//完整实例
   var xhr;
   try{
       xhr= new XMLHttpRequest();
   }catch(e){
       xhr= new ActiveXObject('Microsoft.XMLHTTP'); //IE6
   }
   
   //绑定请求状态变化事件
   xhr.onreadystatechange=function(){
        if(xhr.readystate==4){
            if(xhr.status==200){
                alert(xhr.responseText);
            }else{
            
            }
        }
   }

   //get方式发送数据
   xhr.open('GET','1_get.php?name='+encodeURI("郑骥")+'&age=25&'+new Date().getTime(),true);
   xhr.send();
   /*
    * get方式的两个问题：
    * 1.缓存问题，使用时间戳解决
    * 2.中文编码问题，使用encodeURI进行编码
    */
 
   //post方式发送数据
   xhr.open('POST','2_post.php',true);
   xhr.setRequestHeader('content-type','application/x-www-form-urlencoded'); //申明发送数据类型
   xhr.send('name=郑骥&age=25')
   /*
    *post方式注意：
    * 1.必须设置请求头信息
    * 2.发送的数据作为send()的参数
    */
    
//完整实例 END


```
创建AJAX过程：  
(1) 创建XMLHttpRequest对象,也就是创建一个异步调用对象      
(2) 创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息      
(3) 设置响应HTTP请求状态变化的函数  
(4) 发送HTTP请求  
(5) 获取异步调用返回的数据     
(6) 使用JavaScript和DOM实现局部刷新   

参考：
http://www.imooc.com/video/5913   
http://www.runoob.com/ajax/ajax-tutorial.html   
https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest  
