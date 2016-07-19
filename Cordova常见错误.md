# Cordova常见错误

1. when remove plugin,get error  
    `cordova plugin remove cannot read property 'buffered' of undefined`
    cordova bug,凡是修改plist的plugin卸载都有这个问题.
    [参考](https://github.com/jeduan/cordova-plugin-facebook4/issues/49)
2. 
```error
Permission Denial: starting Intent { act=android.media.action.IMAGE_CAPTURE flg=0x3 cmp=com.android.camera/.Camera clip={text/uri-list U:file:///storage/emulated/0/Android/data/com.bokesoft.wanhua/cache/.Pic.jpg} (has extras) } from ProcessRecord{e8d655f 25072:com.bokesoft.wanhua/u0a107} (pid=25072, uid=10107) with revoked permission android.permission.CAMERA
```
在MIUI 7.5.6中,cordova-plugin-camera会报告不能获取权限的问题。

在"安全中心"--"应用权限管理"--"相应app"--"相机",此项权限的值是"询问",在MIUI 6.4.7中OK,在MIUI 7.5.6中直接拒绝。

解决办法: 如果获得权限失败,提示用户修改"询问"为"允许"。