[[下载并安装MongoDB]]

[yapi 部署官网操作链接](https://hellosean1025.github.io/yapi/devops/index.html)

1. 创建文件夹yapi
2. 进入刚刚创建的文件夹 `cd yapi`
3. `git clone --depth=1 https://github.com/YMFE/yapi.git vendors`
4. `cp vendors/config_example.json ./config.json`
5. 配置config.json 文件为MongoDB设置的用户![[Pasted image 20230219222920.png]]![[Pasted image 20230219222826.png]]![[Pasted image 20230219223007.png]]
```bash
cd vendors
npm install --production --registry https://registry.npm.taobao.org
npm run install-server //安装程序会初始化数据库索引和管理员账号，管理员账号名可在 config.json 配置
node server/app.js //启动服务器后，请访问 127.0.0.1:{config.json配置的端口}，初次运行会有个编译的过程，请耐心等候
```
![[Pasted image 20230219223159.png]]