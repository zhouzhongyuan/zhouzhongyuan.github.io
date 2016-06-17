# Cordova常见错误

1.when remove plugin,get error  
    `cordova plugin remove cannot read property 'buffered' of undefined`
    cordova bug,凡是修改plist的plugin卸载都有这个问题.
    [参考](https://github.com/jeduan/cordova-plugin-facebook4/issues/49)