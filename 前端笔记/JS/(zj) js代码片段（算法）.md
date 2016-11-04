### 数组去重
- **利用Array.prototype.indexOf()** 

```js
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

- **利用Object特性**  
\- **限制**：只能返回新数组，不能在原数组上修改  
\- **限制**：数组中的数字和数值字符串视为等价，即 2 和 '2' 视为互相重复

```js
function uniq(arr){
   var obj={};
   var returnArr=[];
   for(var i=0,len=arr.length;i<len;i++) {
    if(!obj[arr[i]]) {
      obj[arr[i]] = true;
      returnArr.push(arr[i]);
    }
   }
   return returnArr;
}
var arr=[0,2,1,'2',7,1,0];
console.log( uniq(arr) ); // [0,2,1,7]
```


### 数组随机排序
- **不完全随机(限数值类型)**    

```js
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

- **完全随机(不限值类型)**

```js
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

### 创建值均为"a"，长度为1000的数组(限字符串)
```js
function newArr(str,length){
    return new Array(length+1).join(str).split("");
}
```

### 输出字符串中重复次数最多的字符及其次数
- **利用String.prototype.split() 和 Array.prototype.join()**

```js
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

- **利用Object特性**

```js
function maxOfStr(str){
    var max_times=0,max_char,
    obj={};
    
    for(var i=0,len=str.length;i<len;i++){
        if(obj[str.charAt(i)] === undefined){
            obj[str.charAt(i)]=1;
        }else{
            obj[str.charAt(i)]++;
        }
    }
    
    for(var key in obj){
        if(obj[key]>max_times){
            max_times=obj[key];
            max_char=key;
        }
    }
    
    return {
        max_char:max_char,
        max_times:max_times
    }
}
```

### 冒泡排序
\- 思路：参考某个元素值，将小于它的值，放到左数组中，大于它的值的元素就放到右数组中，然后递归进行上一次左右数组的操作

```js
function bubbleSort(arr) {  
    for(var i = 0,len=arr.length;i<len-1;i++) {
        for(var  j = i+1;j<len;j++) { 
          if(arr[i]>arr[j]) {
                var  tem = arr[i];
                arr[i] = arr[j];
                arr[j] = tem;
            }
        }
    }
    return arr;
}
```
### 不借助临时变量，进行两个整数的交换
\- 思路：主要是利用 + - 去进行运算，类似 a = a + ( b - a) 实际上等同于最后 的 a = b

```js
function swap(a , b) {  
  b = b - a;
  a = a + b;
  b = a - b;
  return [a,b];
}
```
### 

