#### 数组去重

```
function uniq(arr,returnNew){
   //默认修改原数组;returnNew参数为true时不修改原数组，而是返回新数组
   if(returnNew){
        arr=arr.concat();
   }
   for(var i=0;i<arr.length;i++){
        //Array.prototype.indexOf():ES5方法;内部为全等匹配
        if( arr.indexOf(arr[i])!==i ){
            arr.splice(i,1);
            i--;
        }
   } 
   return arr;
}
var arr=[0,2,1,'2',7,1,0];
console.log( uniq(arr) ); // [0,2,1,'2',7]

```
#### 数组随机排序
    ##### 不完全随机(限数值类型)
        
    ```
    function random_arr(arr，returnNew){
         //默认修改原数组;returnNew参数为true时不修改原数组，而是返回新数组
        if(returnNew){
            arr=arr.concat();
        }
        arr.sort(function(a,b){
            return ( Math.random()-0.5 );
        });
    }
    ```
   
    ##### 完全随机(不限值类型)

    ```
    function randomArr(arr,returnNew){
        //默认修改原数组;returnNew参数为true时不修改原数组，而是返回新数组
        if(returnNew){
            arr=arr.concat();
        }
	    var len=arr.length;
	    var random;
	    while(len>0){
		    random=Math.floor( Math.random()*len );
		    arr.push( arr[random] );
		    arr.splice(random,1);
		    len--;
	    }
    }
    ```
#### 创建值均为"a"，长度为1000的数组(限字符串)
    
```
function newArr(str,length){
    return new Array(length+1).join(str).split("");
}
```
#### 输出字符串中重复次数最多的字符及其次数

```
function maxOfStr(str){
  var max_times=0,max_char,
  str_arr=[],charNum;
  while(str.length){
      str_arr=str.split(str[0]);
      charNum=str_arr.length-1;
      if(charNum>max_times){
          max_times=charNum;
          max_char=str[0];
      }
      str=str_arr.join("");
  }
  return {
    max_char:max_char,
    max_times:max_times
  }
}

var str="11333331hhdsafdsiiisd";
maxOfStr(str);  // { max_char:"3",max_times:5 }

```
#### 获取元素相对文档左上角的距离
 
```
function getPos(ele){
    var left=0;
    var top=0;
    while(ele && ele.offsetParent!=null){
        left+=ele.offsetLeft;
        top+=ele.offsetTop;
        ele=ele.offsetParent;
    }
    return {
        left:left,
        top:top
    }
}
```

#### 将时间转化为14位数值字符串

```
function timeToDigit(dateStr){
  dateStr=dateStr.replace(/[^\d]+/g,"");
  var len=dateStr.length;
  if(len<14){
    dateStr=dateStr+( new Array(14-len+1).join("0"));
  }
  return dateStr;
}
```
#### 将14位数值字符串转为对象

```
/***将14位数值字符串转为对象: timeObj--时间对象 ,timeStr--指定格式时间字符串
 *
 * @params opts(对象): type--输出时间格式  time--需要转换的纯数值字符串（14位）
 *
 */
function timeFormat(opts){
  var type=opts.type;
  var time=opts.time+"";
  //type必须为格式字符串，形似 "yyyy-mm-dd hh:ff:ss"
  type=type.trim();
  //提取分隔符 separators为分隔符数组
  var separators=[];
  separators.push( type.match( /[^ymdhfs]*(?=yyyy)/ ) ? type.match( /[^ymdhfs]*(?=yyyy)/ ).join("") : "" );
  separators.push( type.match( /[^ymdhfs]*(?=mm)/ ) ? type.match( /[^ymdhfs]*(?=mm)/ ).join("") : "" );
  separators.push( type.match( /[^ymdhfs]*(?=dd)/ ) ? type.match( /[^ymdhfs]*(?=dd)/ ).join("") : "" );
  separators.push( type.match( /[^ymdhfs]*(?=hh)/ ) ? type.match( /[^ymdhfs]*(?=hh)/ ).join("") : "" );
  separators.push( type.match( /[^ymdhfs]*(?=ff)/ ) ? type.match( /[^ymdhfs]*(?=ff)/ ).join("") : "" );
  separators.push( type.match( /[^ymdhfs]*(?=ss)/ ) ? type.match( /[^ymdhfs]*(?=ss)/ ).join("") : "" );
  separators.push( type.split("ss")[1] || "" );
  //需要返回的时间单位 units为时间单位字符串
  var units=type.split(/[^a-zA-Z]+/).join("");
  //提取各单位时间
  var year=units.indexOf("y") !== -1 ? time.substr(0,4) : "";
  var month=units.indexOf("m") !== -1 ? time.substr(4,2) : "";
  var day=units.indexOf("d") !== -1 ? time.substr(6,2) : "";
  var hour=units.indexOf("h") !== -1 ? time.substr(8,2) : "";
  var min=units.indexOf("m") !== -1 ? time.substr(10,2) : "";
  var sec=units.indexOf("s") !== -1 ? time.substr(12,2) : "";
  var timeStr=separators[0]+year+separators[1]+month+separators[2]+day+separators[3]+hour+separators[4]+min+separators[5]+sec+separators[6];
  return {
    timeObj:{
      year:year,
      month:month,
      day:day,
      hour:hour,
      min:min,
      sec:sec
    },
    timeStr:timeStr
  }

}
```
#### 数据类型判断

```
function zj_typeof(data){
   var type=typeof data;
   type=type.toLowerCase();
   if( type === "object"){
     type=Object.prototype.toString.call( data ).slice(8,-1).toLowerCase();
   }
   return type;
}
```


#### 类似jquery的jQuery.extend()的方法

```
/*** obj扩展方法(类似jQuery.extend)，返回被扩展的对象扩展之后的状态,考虑数组和对象这两种情况
 *
 * @param deep (boolean) 是否深度扩展 (可省略，默认false)
 * @param origin (object) 被扩展的对象
 * @param extra (object) 用来扩展的对象
 *
 */
function extend(){
  var agrs=arguments;
  debugger;
  var deep,origin,extra;
  var length=agrs.length;
  var start=0;
  if(typeof agrs[0] === "boolean"){
    deep=agrs[0];
    origin=agrs[1];
    start=2;
    length--;
  }else{
    deep=false;
    origin=agrs[0];
    start=1;
  }
  extra=agrs[start];
  function loop(_origin,_extra){
    //分两种情况，数组或对象
    if( typeof _origin === "object" && typeof _extra === "object" ){
      if( zj_typeof(_origin) === "object" && zj_typeof(_extra) === "object" ){
        for(var key in _extra){
          //被扩展的对象/数组对应的键值没有时或origin和extra类型不同时，origin对应key设为空对象或数组
          if( ( !_origin[key] && _origin[key]!==0 )  || zj_typeof(_origin[key]) !== zj_typeof(_extra[key]) ){
            if( zj_typeof(_extra[key]) === "array" ){
              _origin[key]=[];
            }else if( zj_typeof(_extra[key]) === "object" ){
              _origin[key]={};
            }
          }

          if( deep && typeof _origin[key] ==="object" && typeof _extra[key] ==="object" ){
            loop( _origin[key],_extra[key] );
          }else{
            _origin[key]=_extra[key];
          }
        }
      }else if( zj_typeof(_origin) === "array" && zj_typeof(_extra) === "array" ){
        var originLen=_origin.length;
        var extraLen=_extra.length;
        if(originLen>extraLen){
          _origin.splice(extraLen,originLen-extraLen);
        }
        for(var i=0,len=_extra.length;i<len;i++){
          //被扩展的对象/数组对应的键值没有时或origin和extra类型不同时，origin对应key设为空对象或数组
          if( ( !_origin[i] && _origin[i]!==0 )  || zj_typeof(_origin[i]) !== zj_typeof(_extra[i]) ){
            if( zj_typeof(_extra[i]) === "array" ){
              _origin[i]=[];
            }else if( zj_typeof(_extra[i]) === "object" ){
              _origin[i]={};
            }
          }

          if( deep && typeof _origin[i] ==="object" && typeof _extra[i] ==="object" ){
            loop( _origin[i],_extra[i] );
          }else{
            _origin[i]=_extra[i];
          }
        }
      }
    }
    //检测参数个数
     start++;
     if(start>length){
       return origin;
     }
     loop(origin,agrs[start]);
  }
  loop(origin,extra);
  return origin;
}

``` 
#### 对象深层复制

```
// 1.使用上面封装的 extend(true,{},obj)

// 2.使用JSON.parse()和JSON.stringify()
function deepCopy(obj){
    return JSON.parse( JSON.stringify(obj) ); 
}
```











   




