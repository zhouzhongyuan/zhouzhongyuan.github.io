1. 如何使用命令行导入p12证书
    ```
    security import app证书.p12 -k ~/Library/Keychains/login.keychain -P 1
    ```
    app证书.p12:p12文件所在的路径
    1(注释:-P后面的1): p12文件的密码
2. 导入证书之后,每次打包都会弹窗怎么办?
![Alt text](ios/pack/codesign-error.png "Optional title")
    手动解决方法如下:
    ![Alt text](ios/pack/codesign-deal.png "Optional title")
    命令行:
    添加证书时 添加参数
    ```
    -T /usr/bin/codesign
    ```
    完整命令如下
    ```
    security import app证书.p12 -k ~/Library/Keychains/login.keychain -P 1 -T /usr/bin/codesign
    ```
2. 删除证书
http://stackoverflow.com/questions/7678057/remove-private-key-from-mac-os-x-keychain-using-terminal