
```
　　var getClipText = function() {
        var t = "";
        return window.getSelection ? t = window.getSelection().toString() : window.document.selection && "Control" !== window.document.selection.type && (t = window.document.selection.createRange().text),
            t;
    };
    document.addEventListener("copy",function(event){
    	var clipboard,setDataText,setDataHtml,getDataText;
    	if(event.clipboardData){
    		clipboard=event.clipboardData;
    		//利用bind实现函数柯里化
    		setDataText=clipboard.setData.bind(clipboard,"text/plain");
    		setDataHtml=clipboard.setData.bind(clipboard,"text/html");
    		getDataText=clipboard.getData.bind(clipboard,"text/plain");
    	}else if(window.clipboardData){
    		//IE
    		clipboard=window.clipboardData;
    		setDataText=clipboard.setData.bind(clipboard,"text");
    	}
		var text=getClipText()+" \n版本信息：.....";
	    setDataHtml("<div>" + text + "</div>");
	    setDataText(text);
	    //Firefox、Safari 和 Chrome 只允许在 onpaste 事件处理程序中访问 getData() 方法,(除非之前已调用setData)
	    console.log( getDataText("text/plain") );
	    //必须阻止默认事件，原因暂时不详
	    return event.preventDefault();
    });
```
参考：
    \- **js高三**       