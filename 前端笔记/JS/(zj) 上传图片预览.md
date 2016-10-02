### 兼容IE6的图片预览
```
【html代码】：
<input id="file_upload" type="file" />
<div class="image_container">
    <img id="preview" width="60" height="60">
</div>

代码如下利用html5实现:几乎兼容所有主流浏览器，当然IE必须是IE 6以上
【jquery代码】
$(function() {
    $("#file_upload").change(function() {
        var $file = $(this);
        var fileObj = $file[0];
        var windowURL = window.URL || window.webkitURL;
        var dataURL;
        var $img = $("#preview");
 
        if(fileObj && fileObj.files && fileObj.files[0]){
            dataURL = windowURL.createObjectURL(fileObj.files[0]);
            $img.attr('src',dataURL);
        }else{
           dataURL = $file.val();
           var imgObj = document.getElementById("preview");
        // 两个坑:
        // 1、在设置filter属性时，元素必须已经存在在DOM树中，动态创建的Node，也需要在设置属性前加入到DOM中，先设置属性在加入，无效；
        // 2、src属性需要像下面的方式添加，上面的两种方式添加，无效；
            imgObj.style.filter = "progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale)";
            imgObj.filters.item("DXImageTransform.Microsoft.AlphaImageLoader").src = dataURL;
     
        }
    });
});

```


```
            //原生ajax
            var xhr = new XMLHttpRequest();
            //发送完成并成功事件
            xhr.onload = function() {
                if (xhr.responseText == 1) {
                    //模态框提示
                    $(".modal-body>.modal-main").html("发布成功");
                    myModal.modal("show");
                    setTimeout(function() {
                        location.reload(true);
                    }, 1000);
                } else {
                    //模态框提示
                    $(".modal-body>.modal-main").html("发布失败");
                    myModal.modal("show");
                }
            };
            //提交失败事件
            xhr.onerror = function() {
                //模态框提示
                $(".modal-body>.modal-main").html("发布失败");
                myModal.modal("show");
            };
            //post方式提交，异步
            xhr.open('post', JSV.PATH_SERVER + 'Index/post_file', true);
            //设置头部信息（post方式必须）
            xhr.setRequestHeader('X-Request-With', 'XMLHttpRequest');
            //获取files对象
            var uploadFileBtn = $("#uploadFileBtn");
            var filesObj = uploadFileBtn[0].files;
            // //通过FormData来构建提交文件数据
            var formData = new FormData();
            //调用 append(name，value) 方法并传入相应的 File 对象作为参数(假设只有一个上传文件)
            formData.append("photo", filesObj[0]);
            var formTextData = requestData(formObj);
            for (var key in formTextData) {
                formData.append(key, formTextData[key]);
            }
            //将formData作为参数调用send()方法
            xhr.send(formData);
```
### 现代主流浏览器(IE10+):参考高三

```
// 【html代码】：
<input id="file_upload" type="file" />
<div class="image_container">
    <img id="preview" width="60" height="60">
</div>

// 【js代码】：
// 1. 将图片转为base64,可将base64作为ajax传送数据
var upload=document.querySelector("#file_upload");
var preview=document.querySelector("#preview");
upload.onchange=function(){
    var file=this.files;
    var reader = new FileReader();
    var (var i=0,len=files.length;i++){
        reader.readAsDataURL(target.files[i]);
        reader.onload =function(e){
            preview.src=reader.result;
        };
    }
}
// 2.使用对象url
var upload=document.querySelector("#file_upload");
var preview=document.querySelector("#preview");
upload.onchange=function(){
    var file=this.files;
    var windowUrl=window.URL || window.webkitURL;
    var (var i=0,len=files.length;i++){
        preview.src=windowUrl.createObjectURL(files[i]);
    }
}
```
