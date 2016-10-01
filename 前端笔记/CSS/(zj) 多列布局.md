- ### 定宽-自适应
    - #### float + margin
        
    ```
    .left{float:left; width:100px;}
    .right{margin-left:120px;}
    ```
    - #### float + margin + fix
        
    ```
    <div class="left"></div>
    <div class="right-fix">
        <div class="right"></div>
    </div>
    
    .left{float:left; width:100px; position: relative;}
    .right-fix{float:right; width:100%; margin-left:-100px;}
    .right{margin-left:120px;}
    
    // 外层再包裹一个容器
    // 兼容性很好，但是多了层 right-fix 的结构
    ```
    - #### float + overflow
        
    ```
    .left{float:left; width:100px; margin-right: 20px;}
    .right{overflow:hidden;}
    ```
    - #### table
        
    ```
    .parent{display:table; width:100%; table-layout:fixed;}
    .left,.right{display:table-cell;}
    .left{width:100px; padding-right:20px;}
    ```
    - #### flex
        
    ```
    .parent{display:flex;}
    .left{width:100px; margin-right:20px;}
    .right{flex:1;}
    ```
- ### 不定宽-自适应
    - #### float + overflow
        
    ```
    .left{float:left; margin-right:20px;}
    .right{overflow:hidden;}
    ```
    - #### table
        
    ```
    .parent{display:table; width:100%;}
    .left,.right{display:table-cell;}
    .left{width:0.1%; padding-right:20px;}
    ```
    - #### flex
        
    ```
    .parent{display:flex;}
    .left{margin-right:20px;}
    .right{flex:1;}
    ```

参考：https://segmentfault.com/a/1190000003113119



