在apifox创建项目，定义接口，获取base url
![[Pasted image 20230220100320.png]]

在webpack配置的devServer的proxy中配置
[proxy配置](https://blog.csdn.net/weixin_53474595/article/details/127746519)

>[!INFO] 每次Mock都需要启动apifox服务
```js
const webpackConfigDev = {
	devServer: {
		proxy: {
            '/': 'http://127.0.0.1:4523/m1/883443-0-default/', // 监听以/开头的接口，把axios请求中前面的本地服务器地址改为后端接口地址，实际发送给后端的请求是：http://localhost:8080/abc/def --> http://XX.XX.XX.XX:8081/abc/def
        },
	}
}
```

在项目中使用

```js
axios.get('/ad/index/gray').then((res) => { // 以/开头的请求，配合proxy中的配置/
	console.log(res.data);
}).catch((err) => {
	console.log(err);
});
```
