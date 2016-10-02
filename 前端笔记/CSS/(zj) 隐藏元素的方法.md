#### 隐藏元素的几种方法
    ##### display:none; (完全隐藏：视觉和屏幕阅读器不可见)
        \- 不占位  
        \- 不支持动画
    ##### visiblity:hidden; (完全隐藏)
        \- 占位 
        \- 能够实现动画效果  
        \- 不会响应任何用户交互  
        \- 读屏软件中也会被隐藏  
        \- 一个元素的 visibility 被设置为 hidden，同时想要显示它的某个子孙元素，只要将子元素的 visibility 显式设置为 visible 即可（即外部元素虽然设置了visibility:hidden并不能隐藏内部元素设置了visibility:visible的元素）,**子元素上的交互可以冒泡到父元素上**  
        \- visiblity 默认值：visible  
        \- visibility 设为hidden的元素的后代元素使用visibility:inherit替代visibility:visible避免意外地显示内容
    ##### opcity:0; (视觉上隐藏)
        \- 占位 
        \- 会被读屏软件阅读
        \- 能够实现动画效果    
        \- 任何 opacity 属性值小于 1 的元素也会创建一个新的堆叠上下文（stacking context）
    ##### 绝对定位 (视觉上隐藏，且脱离文档流，不占空间)
        \- 将元素的 top 和 left 设置成足够大的负数，使它在屏幕上不可见  
        \- 避免使用这个方法去隐藏任何可以获得焦点的元素
    ##### clip (视觉上隐藏)
        \- 元素必须绝对定位(absolute)或固定定位(fixed)  
        \- 代码类似如下  
        \- 类似的新特性clip-path（可使用clip-path:inset(100%)来替代clip:rect(0 0 0 0)，兼容性差）
        ```
            .hide 
            {
                position:absolute;
                clip:rect(0,0,0,0); //或者 clip-path:inset(100%)
            }
        ```
    ##### 将元素的font-size、line-height、width和height设置为0 (视觉上隐藏)
    ##### 设置元素的 transform 的 translateX 或者 translateY 的值为-100% (视觉上隐藏)
    ##### 给元素声明一个hidden属性值（H5）(完全隐藏)
        \- 元素间接通过display:none;隐藏  
    ##### 在元素上设置aria-hidden="true" (语义上隐藏：只是在屏幕阅读器中隐藏)
参考：  
https://www.h5jun.com/post/five-ways-to-hide-elements-in-css.html  
http://www.w3cplus.com/css/hidden-dom-element.html