# 单向居中
### 1. 水平居中
#### 块元素在父元素中水平居中：

```
margin : 0 auto;
```
#### 元素中的单行文字水平居中：

```
text-align:center;
```
### 2. 垂直居中
#### 元素中的单行文字垂直居中：
设置元素高度（height）和行高（line-height）值相同
# 水平垂直居中
### 图片水平垂直居中

```css
/* IE8+ */
div.imgWrap {
  height:240px;
  line-height: 240px;
  font-size: 0;
  text-align : center;
}
img {
  vertical-align: middle;
}

/* IE8+（不推荐）*/
.imgWrap{  
  height:400px ;
  text-align : center
}
.imgWrap:after{
  content:"" ;
  display: inline-block ;
  height:100%;
  width: 0 ;
  vertical-align: middle;
}
img{
  vertical-align: middle;
}
```
### 多行文本水平垂直居中

```css
.box{
  line-height:250px;
  text-align:center;
}
.box>.textWrap{
  display:inline-block;
  line-height:normal;
  text-align:left;
  vertical-align:middle;
}
```
### position + margin (1) (定宽高)

```css
/** 绝对定位（absolute）或固定定位（fixed）
* 原理：设置left，right，top，bottom均为0；margin值设为auto，注意不是0 auto；
* 注意：必须设置高宽。若未设置高宽，则left:0;right:0; 将元素宽度变为父元素宽度；
top:0;bottom:0; 将元素高度变为父元素高度；
*/

/* IE8+ */
.parent{
  position:relative
}
.child{
  position:absolute;
  width:100px;
  height:100px;
  left:0;
  right:0;
  top:0;
  bottom:0;
  margin:auto;
}

```
### position + margin (2) (定宽高)

```css
/* IE6+ */
.parent{
  position:relative
}
.child{
  position:absolute;
  width:100px;
  height:100px;
  /*left,right百分比基于父元素尺寸*/
  left:50%;
  right:50%;
  margin-left:-50px;
  margin-top:-50px;
}
```
### position + transform

```css
/* IE9+ */
.parent{
  position:relative;
  height:200px; /* 父容器必须设置高度 */
}
.child{
  position:absolute;
  width:100px;
  height:100px;
  left:50%;
  right:50%;
  /*translate百分比基于元素自身尺寸*/
  /*margin百分比基于父元素尺寸*/
  transform:translate(-50%;-50%);
}
```

### calc
```css
/* IE9+ */
.parent{
  position:relative;
  height:200px; /* 父容器必须设置高度 */
}
.child{
  position:absolute;
  width:100px;
  height:120px;
  left:calc(50% - 50px);
  right:calc(50% - 60px);;
}
```

### table + vertical-align + margin

```css
/* IE8+ */
/* 注意：table类元素宽度由子元素撑开 */
.parent{
  display:table;
  margin:0 auto;
}
.child{
  display:table-cell;
  vertical-align:middle;
}
```
### flexbox (1)

```css
.parent{
  display:-webkit-flex;
  justify-content:center; /* 子元素水平居中 */
  align-items:center; /* 子元素垂直居中 */
}
```
### flexbox (2)

```css
.parent{
  display:-webkit-flex;
  width: 200px;
  height: 200px;
}

.child{
  width: 100px;
  height: 100px;
  margin: auto;
}
```

### table-cell + vertical-align + text-align + inline-block   

```css
/* IE8+ */
.parent{
  text-align:center;
  display:table-cell;
  vertical-align:middle;
}
.child{
  display: inline-block;
  vertical-align:middle;
}
```
### position + table-cell

```html
<!-- IE6+ -->

<!-- html -->
<div class="table">
<div class="tableCell">
<div class="content">不固定宽高，自适应</div>
</div>
</div>

<!-- css -->
<style>
  .table {
    height: 200px; /*高度值不能少*/
    width: 200px; /*宽度值不能少*/
    display: table;
    position: relative;
    float:left;
  }      

  .tableCell {
    display: table-cell;
    vertical-align: middle;
    text-align: center;        
    *position: absolute;
    padding: 10px;
    *top: 50%;
    *left: 50%;
  }
  .content {
    *position:relative;
    *top: -50%;
    *left: -50%;
  }
</style>


```

参考：  
http://www.cnblogs.com/xianyulaodi/p/5863305.html
