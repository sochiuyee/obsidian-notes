[YApi 部署步骤](https://hellosean1025.github.io/yapi/devops/index.html)

###### 1. 安装MongoDB
[官网安装地址](https://www.mongodb.com/try/download/community)
[安装教程](http://c.biancheng.net/mongodb2/install-on-windows.html)
[解决MongoDB指令mongo不是内部指令问题](https://blog.csdn.net/weixin_51293984/article/details/128076353?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-128076353-blog-127907658.pc_relevant_multi_platform_whitelistv3&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-128076353-blog-127907658.pc_relevant_multi_platform_whitelistv3&utm_relevant_index=1)

	1. windows配置环境变量
		1. 找到MongoDB安装的bin目录
		2. 在环境变量的path中添加MongoDB的bin路径
	2. 解决mongoDB 6.0 以上mongo不是指令问题
		1. 下载MongoDB Shell
		2. 下载后解压，直接把这个解压后的文件复制到Mongo6的安装路径里面
		3. 配置mongodb shell bin目录到环境变量中

配置MongoDB 环境变量
![[Pasted image 20230213101422.png]]
![[Pasted image 20230213101523.png]]

![[Pasted image 20230213101610.png]]

![[Pasted image 20230213101640.png]]

解决mongo 不是内部指令
1. 把下载的MongoDB shell 放置在mongodb的安装路径下
![[Pasted image 20230213102023.png]]

1. 配置MongoDB shell 的bin 环境变量![[Pasted image 20230213102136.png]]
![[Pasted image 20230213102204.png]]

###### 连接数据库
`mongosh`

###### 显示当前已经建好的数据库
`show dbs`

###### 创建数据库表
`use yapidb`

###### 创建用户，并为用户添加相关数据库的权限

```js
// 创建数据库用户并为其赋角色
db.createUser({user:"admin", pwd:"admin",roles:[{role:"dbAdmin",db:"yapidb"}]})

// 将数据库为用户授权db.auth(用户名，密码)
db.auth("admin","admin")
```

