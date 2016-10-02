### screen对象
  #### 获取屏幕的高宽

```
screen.width         //屏幕的宽
screen.height        //屏幕的高
screen.availWidth    //屏幕可用宽度   屏幕的像素高度 - 系统部件高度
screen.availHeight   //屏幕可用高度   屏幕的像素宽度 - 系统部件宽度
```
### window对象
  #### 获得窗口位置及大小

```
window.screenTop            //窗口顶部距屏幕顶部的距离

window.screenLeft           //窗口左侧距屏幕左侧的距离

window.innerWidth           //窗口中可视区域(viewpoint)的宽度
alert(window.innerWidth);   //chrome 1366 ff 1366 ie 1366

window.innerHeight          //窗口中可视区域(viewpoint)的高度该值与浏览器是否显示菜单栏等因素有关
alert(window.innerHeight);  //chrome 643  ff 657  ie 673

window.outerWidth           //浏览器窗口本身的宽度(可视区域宽度+浏览器边框宽度)
alert(window.outerWidth);   //chrome 1366 ff 1382 ie 1382  
                            //说明chrome在最大化时浏览器窗口没有边框宽度,非最大化时有8px边框
                            //ff和ie上下左右有8px的边框宽度
                            
window.outerHeight          //浏览器窗口本身的高度
alert(window.outerHeight);  //chrome 728 ff 744 ie 744
```
### element对象
    #### 当不出现滚动条时

    ```
    body{margin:0;}
    #demo{
        width:100px;
        height:100px;
        padding:10px;
        border:20px;
        margin:30px;
        background-color:red;
    }
    <div id="demo">123456789 123456789</div>
    ```
    ##### clientWidth :  在页面上返回内容的可视宽度（不包括边框，边距或滚动条）
    ##### clientHeight : 在页面上返回内容的可视高度（不包括边框，边距或滚动条）

    ```
    clientWidth = 2*padding + width - scrollbarWidth     
    console.log(document.getElementById('demo').clientWidth); //120 此时scrollbarWidth=0

    clientHeight = 2*padding + height - scrollbarHeight 
    console.log(document.getElementById('demo').clientHeight); //120 此时scrollbarWidth=0
    ```
    ##### offsetWidth:返回元素的宽度包括边框和填充，但不包括边距
    ##### offsetHeight:返回元素的高度包括边框和填充，但不包括边距

    ```
    offsetWidth = 2*border + 2*padding + width  
    console.log(document.getElementById('demo').offsetWidth)    //160

    offsetHeight = 2*border + 2*padding + height  
    console.log(document.getElementById('demo').offsetHeight)   //160
    ```
    ##### offsetLeft: 获取对象元素边界的左上角顶点相对于offsetParent的左上角顶点的水平直偏移量
    ##### offsetTop: 获取对象元素边界的左上角顶点相对于offsetParent的左上角顶点的竖直偏移量

    ```
    console.log(document.getElementById('demo').offsetLeft)    //30
    console.log(document.getElementById('demo').offsetTop)    //30
    ```  
    #### 当出现滚动条时
  
    ```  
    body{
        margin:0;
        padding:20px;
        width:1000px;
        height:500px;
    }
    <div id="demo">123456789123456789</div>
    ```
    ##### scrollWidth: 返回元素的整个宽度（包括带滚动条的隐蔽的地方）
    ##### scrollHeight: 返回整个元素的高度（包括带滚动条的隐蔽的地方）

    ```
    scrollWidth = 2*padding + width    
    console.log(document.body.scrollWidth)    //1040

    scrollHeight = 2*padding + height   
    console.log(document.body.scrollHeight)   //540
    ```
    ##### scrollTop: 向下滑动滚动块时元素隐藏内容的高度。不设置时默认为0，其值随着滚动块滚动而变化
    ##### scrollLeft: 向右滑动滚动块时元素隐藏内容的宽度。不设置时默认为0，其值随着滚动块滚动而变化

### event对象
    ##### Event 对象代表事件的状态，比如事件在其中发生的元素、键盘按键的状态、鼠标的位置、鼠标按钮的状态。

    **event.pageX** : 相对整个页面的坐标，以页面的左上角为坐标原点到鼠标所在点的水平距离（IE9+，低版本IE可用 event.clientX + (document.body.scrollLeft || document.documentElement.scrollLeft)计算出 ）  
    **event.pageY** : 相对整个页面的坐标，以页面的左上角为坐标原点到鼠标所在点的垂直距离（IE9+，低版本IE可用 event.clientY + (document.body.scrollTop || document.documentElement.scrollTop)计算出 ）

    **event.clientX** : 相对可视区域的坐标，以浏览器可视区域左上角为坐标原点到鼠标所在点的水平距离  
    **event.clientY** : 相对可视区域的坐标，以浏览器可视区域左上角为坐标原点到鼠标所在点的垂直距离

    **event.screenX** : 相对电脑屏幕的坐标，以屏幕左上角为坐标原点到鼠标所在点的水平距离  
    **event.screenY** : 相对电脑屏幕的坐标，以屏幕左上角为坐标原点到鼠标所在点的垂直距离

    **event.offsetX** : 相对于自身的坐标，以自身的padding左上角为坐标原点到鼠标所在点的水平距离（IE）  
    **event.offsetY** : 相对于自身的坐标，以自身的padding左上角为坐标原点到鼠标所在点的水平距离（IE）

    **window.pageXOffset**	设置或返回当前页面相对于窗口显示区左上角的 X 位置(IE不支持)  
    **window.pageYOffset**  设置或返回当前页面相对于窗口显示区左上角的 Y 位置(IE不支持)

参考: http://www.cnblogs.com/jesse131/p/5709285.html





