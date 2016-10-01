- #### firefox中滚轮事件为DOMMouseScroll，其他浏览器为mousewheel
- #### firefox中使用event.detail属性，其他浏览器中使用event.wheeldelta
- #### firefox中属性取值±3，其他浏览器中属性取值±120
- #### firefox种负数表示向上，其他浏览器中正数表示向上

```
// firefox
document.body.addEventListener("DOMMouseScroll", function(event) {

    var direction= event.detail && (event.detail > 0 ? "mousedown" : "mouseup");
    console.log(direction);    
});

// chrome and ie
document.body.onmousewheel = function (event) {
    event = event || window.event;

    var direction = event.wheelDelta && (event.wheelDelta > 0 ? "mouseup" : "mousedown");
    console.log(direction);
};
// jquery 兼容的滚轮事件
$(document).on("mousewheel DOMMouseScroll", function (e) {
                 // chrome & ie
    var oEvent=e.originalEvent;
    var delta = (oEvent.wheelDelta && (oEvent.wheelDelta / 120) || 
                 // firefox
                (oEvent.detail && (oEvent.detail / -3));            

    
    if (delta > 0) {
        // 向上滚
        console.log("wheelup");
    } else if (delta < 0) {
        // 向下滚
        console.log("wheeldown");
    }
});
```
