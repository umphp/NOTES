
```
function Fn1(name,age){
    this.name=name;
    this.age=age;
}
Fn1.prototype.sayhi=function(){
    console.log("hello");
}
function Fn2(name,age,array){
    Fn1.call(this,name,age);
    this.array=[1,2,3];
}
//模拟Object.create()
/*
if( !Object.create ){
    Object.create=function(proto){
        function F(){};
        F.prototype=proto;
        return new F;
    }
}

*/
Fn2.prototype=Object.create(fn1.prototype); //ES5方法
var obj1=new Fn2("john",20);
var obj2=new Fn2("mary",30);
console.log( obj1.name ); // "john"
console.log(obj1.sayhi()); // "hello"
obj1.array.push(4);
console.log(obj1.array); // [1,2,3,4]
console.log(obj2.array); // [1,2,3]
```
参考：  
https://segmentfault.com/a/1190000004730936  