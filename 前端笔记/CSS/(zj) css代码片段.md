#### 单行文本超出显示省略号：
    
```
.newsItem .newsText{
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    width:100px;
}
```
#### 伪类中文字换行

```
div:after{
    content:"公众\A账号";
    white-space:pre;
}
```
#### 文本溢出显示...

```
//单行文本溢出...
.in_a_line{
    overflow:hidden;
    white-space:nowrap;
    text-overflow:ellipsis;
}
//多行文本溢出...
.in_two_line{
    display:-webkit-box !important;
    overflow:hidden;
    text-overflow:ellipsis;
    word-break:break-all;
    -webkit-line-clamp:2; //控制显示行数
    -webkit-box-orient:vertical;
}
```

