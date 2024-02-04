[https://juejin.cn/post/6986888917622456351](https://juejin.cn/post/6986888917622456351)

1.  使用node版本16 使用安装whistle

```js
npm install -g whistle

// 或者直接指定镜像安装：
npm install whistle -g --registry=https://registry.npm.taobao.org
```

2.  启动whistle
`w2 start`

电脑浏览器访问
![[Pasted image 20230420142427.png]]

![[Pasted image 20230420142512.png]]

下载根证书：Whistle 监控界面 -> HTTPS -> Download RootCA  
下载完根证书后点击rootCA.crt文件，弹出根证书安装对话框。

Android：  
用浏览器扫描 whistle 监控界面 **HTTPS** 的二维码下载安装，或者浏览器地址栏 rootca.pro 按提示安装。ca 证书安装完后可以在 Android 手机的“设置” -> “安全和隐私” -> “受信任的凭证” 里查看手机上有没有安装成功。