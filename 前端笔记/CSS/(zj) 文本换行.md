#### word-wrap: 允许长单词或 URL 地址换行到下一行
    \- **normal**　　　　只在允许的断字点换行（浏览器保持默认处理）  
    \- **break-word**　　在长单词或 URL 地址内部进行换行  
    注意：break-word　需要容器设定宽度才会起作用

#### word-break: 通过使用 word-break 属性，可以让浏览器实现在任意位置的换行
    \- **normal**　　　使用浏览器默认的换行规则  
    \- **break-all**　　允许在单词内换行  
    \- **keep-all**　　只能在半角空格或连字符处换行  
#### word-wrap与word-break区别
    ##### word-wrap   
        \- 用来决定允不允许单词内断句的，如果不允许的话长单词就会溢出。  
        \- 最重要的一点是它还是会首先尝试挪到下一行，看看下一行的宽度够不够，不够的话就进行单词内的断句。并且需要容器设置了指定的宽度才会生效。  
        \- 作用范围仅为div这类标准块级元素，th,td这类table元素虽然识别但是没有效果    
    ##### word-break         
        \- **word-break:break-all** 则更变态，因为它断句的方式非常粗暴，它不会尝试把长单词挪到下一行，而是直接进行单词内的断句。  
        \- 作用范围仅为div这类标准块级元素，th,td这类table元素虽然识别但是没有效果  
        \- Firefox,Opera是无法识别word-break  
#### white-space:
    \- **normal**　　默认。空白会被浏览器忽略   
    \- **pre**　　　　空白会被浏览器保留，其行为方式类似HTML中的pre标签  
    \- **nowrap**　　文本不会换行，文本会在在同一行上继续，直到遇到br标签为止 

参考：http://www.wufangbo.com/css-qiang-zhi-huan-hang/



