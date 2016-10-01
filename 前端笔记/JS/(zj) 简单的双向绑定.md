
```
    <div>
		<input type="text" id='dataIn'>  
	    <div id="dataOut"></div>
	</div>　
	<script>
		//思路:利用Object.defineProperty
		//创建一个保存数据的对象data，利用Object.defineProperty，设置set/get方法
		//将输入框的keyup事件和data数据绑定，输入框值变化则data调用set方法，data的set方法又设置div的innerHTML
		function $(sel){
			var result=document.querySelectorAll(sel);
			if(result.length===1){
				result=result[0];
			}
			return result;
		}
		var data={
			_input:""
		};
		Object.defineProperty(data,"input",{
			get:function(){
				return this._input;
			},
			set:function(val){
				this._input=val;
				$("#dataOut").innerHTML=val;
			}
		});
		$("#dataIn").addEventListener("keydown",function(){
			data.input=this.value;
		});
	</script>
```
