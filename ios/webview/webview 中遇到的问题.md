1. 使用cordova 等生成app时,手指长按会出来系统自带的操作(复制,粘贴等)
    全局或者部分div上添加下面的css

    ```css
    -webkit-touch-callout: none;
    -webkit-user-select: none; /* Disable selection/copy in UIWebView */
    ```