## transition
参考：http://www.w3cplus.com/content/css3-transition  

**兼容性**：  
IE10+, Firefox,Chrome 和 Opera支持transition 属性。  
Safari 通过私有属性 -webkit-transition 支持。  


**语法**：
`transition: property duration timing-function delay;`  

**默认值**：
`all 0 ease 0；`

**参数**：
- `transition-property`   
指定CSS属性的name  
**可选值**：none、all、property（定义应用过渡效果的 CSS 属性名称列表，列表以逗号分隔）

- `transition-duration`   
 transition效果需要指定多少秒或毫秒才能完成（注意带单位s / ms）

- `transition-timing-function`   
 指定transition效果的转速曲线  
**可选值**：   
linear（线性渐变）   
ease（慢速开始，然后变快，最后慢速结束）  
ease-in（慢速开始）  
ease-out（慢速结束）  
ease-in-out（慢速开始，慢速结束）  
cubic-bezier(n,n,n,n) （在 cubic-bezier 函数中定义自己的值。可能的值是 0 至 1 之间的数值）

- `transition-delay`  
定义过渡效果开始之前需要等待的时间，以秒或毫秒计（注意带单位s / ms）

```css
a{
     background:#f00;
     color:#0f0;
     -moz-transition: background 0.5s ease-in,color 0.3s ease-out;
     -webkit-transition: background 0.5s ease-in,color 0.3s ease-out;
     -o-transition: background 0.5s ease-in,color 0.3s ease-out;
     transition: background 0.5s ease-in,color 0.3s ease-out;  
}
a:hover{
     background:#0f0;
     color:#f00;
}
```

## animation
参考：http://www.w3cplus.com/content/css3-animation  

**兼容性**：  
IE10+, Firefox,Chrome 和 Opera支持 animation 属性。  
Chrome 和 Safari 通过私有属性 -webkit-animation 支持。  

**语法**：
`animation: name duration timing-function delay iteration-count direction;`  

**默认值**：
`none 0 ease 0 1 normal;`

**参数**：
- `animation-name`   
 @keyframes 动画指定名称   
**可选值**：keyframename、none;

- `animation-duration`   
 动画指定需要多少秒或毫秒完成（注意带单位s / ms）

- `animation-timing-function`   
 设置动画将如何完成一个周期  
**可选值**：   
linear（线性渐变）   
ease（慢速开始，然后变快，最后慢速结束）  
ease-in（慢速开始）  
ease-out（慢速结束）  
ease-in-out（慢速开始，慢速结束）  
cubic-bezier(n,n,n,n) （在 cubic-bezier 函数中定义自己的值。可能的值是 0 至 1 之间的数值）

- `animation-delay`  
设置动画在启动前的延迟间隔。（注意带单位s / ms）

- `animation-iteration-count`  
定义动画的播放次数  
**可选值**：num、infinite

- `animation-direction`  
指定是否应该轮流反向播放动画  
**可选值**：  
normal   
everse（动画反向播放）  
alternate（动画在奇数次（1、3、5...）正向播放，在偶数次（2、4、6...）反向播放）  
alternate-reverse（与alternate相反）  
initial（设置该属性为它的默认值）  
inherit

- `animation-fill-mode`
动画的最后（达到100%）时的状态  
**可选值**：  
backward（回到初始状态）  
forwards（停在最终状态）  
both  
none  


```css
 .spinner{
          width:40px;
          height:40px;
          background-color:green;
          border-radius:100%;
          margin: 100px auto;
          -webkit-animation:fadeOut 1.0s infinite ease-in-out;
          animation:fadeOut 1.0s infinite ease-in-out;
  }
@-webkit-keyframes fadeOut{
    from {-webkit-transform:scale(0.0);}
    50% {-webkit-transform:scale(0.4); }
    to {-webkit-transform:scale(1.0);opacity:0;}
  }
@keyframes fadeOut{
    from{transform:scale(0.0);}
    50% {transform:scale(0.4); }
    to{transform:scale(1.0);opacity:0;}
}
```

## transform
参考：http://www.w3cplus.com/content/css3-transform  

transform往往与transition和@keyframes配合使用实现动画效果

**兼容性**：  
IE10+, Firefox,Chrome 和 Opera支持  transform-origin 属性。  
IE9 支持替代的 -ms-transform-origin 属性（仅适用于 2D 转换）。
Safari 和 Chrome 支持替代的 -webkit-transform-origin 属性（3D 和 2D 转换）    
Opera 只支持 2D 转换  

**语法**：
`transform: none|transform-functions;`  

transform-functions:主要有  **translate（位移）**、**rotate（旋转）**、**scale（缩放）**、**skew（扭曲/歪斜）**、  **matrix（矩阵）**

**默认值**：  
`none;`

### transform-origin  
用来设置元素的运动的基点（参照点）。默认点是元素的中心点

**语法**：`transform-origin: x-axisy-axisz-axis;`

**注意**：使用此属性必须先使用 `transform` 属性  

**参数**：
- `x-axis`  
定义视图被置于 X 轴的何处  
**可选值**：left、center、right、length、%

- `y-axis`
定义视图被置于 Y 轴的何处  
**可选值**：top、center、bottom、length、%

- `z-axis`  
定义视图被置于 Z 轴的何处：length

```css
#div2 {
    padding:50px;
    position: absolute;
    border: 1px solid black;
    background-color: yellow;
    -ms-transform: rotate(45deg); /* IE 9 */
    -ms-transform-origin:20% 40%; /* IE 9 */
    -webkit-transform: rotate(45deg); /* Safari and Chrome */
    -webkit-transform-origin:20% 40%; /* Safari and Chrome */
    -moz-transform: rotate(45deg); /* Firefox */
    -moz-transform-origin:20% 40%; /* Firefox */
    -o-transform: rotate(45deg); /* Opera */
    -o-transform-origin:20% 40%; /* Opera */
    transform: rotate(45deg);
    transform-origin:20% 40%;
}
```

**参考**：
- http://www.zhangxinxu.com/wordpress/2010/11/css3-transitions-transforms-animation-introduction/
