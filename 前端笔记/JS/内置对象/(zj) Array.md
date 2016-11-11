# 1. 创建数组
### 1.1 字面量  
`var arr=[1,2]`
### 1.2 Array构造器  

```js
new Array(size);
new Array(element0, element1, ..., elementn);

new Array(); // []
new Array(2); // [undefined , undefined]
new Array(1,2); // [1,2]
```

# 2. 属性
### 2.1 length
\- 返回数组的长度

# 3. 方法
## 3.1 不修改原数组
### 3.1.1 Array.isArray()
\- 兼容性:IE9+  
\- 判断是否为数组对象  

```js
Array.isArray([1,2]) // true
```
**Polyfill**

```js
if (!Array.isArray) {
  Array.isArray = function(arg) {
    return Object.prototype.toString.call(arg) === '[object Array]';
  };
}
```

### 3.1.2 Array.prototype.concat()
\- 传入的数组或非数组值与原数组合并,组成一个新的数组并返回  

#### 语法
`var new_array = old_array.concat(value1[, value2[, ...[, valueN]]])`
#### 参数
**valueN**  
需要与原数组合并的数组或非数组值
#### 返回值
新的 Array 实例

```js
var arr1=[1,2];

arr1.concat([3,4]); // [1,2,3,4]
arr1  // [1,2]

arr1.concat(3,4); // [1,2,3,4]
arr1  // [1,2]

arr1.concat([3,4],[5,6]); // [1, 2, 3, 4, 5, 6]
arr1  // [1,2]
```

#### 运用:
- **数组浅复制**  
\- 适用场景：数组项为基本类型

```js
var arr1=[1,2];
var arr2=arr1.concat();

arr1[2]=3;
arr1; //[1,2,3]
arr2; //[1,2]

```

### 3.1.3 Array.prototype.concat()
\- 传入的数组或非数组值与原数组合并,组成一个新的数组并返回  

#### 语法
`var new_array = old_array.concat(value1[, value2[, ...[, valueN]]])`
#### 参数
**valueN**  
需要与原数组合并的数组或非数组值
#### 返回值
新的 Array 实例


## 3.2 修改原数组

## 3.3 数组遍历
