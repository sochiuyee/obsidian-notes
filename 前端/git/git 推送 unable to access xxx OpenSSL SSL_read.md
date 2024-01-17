> # Git报错：fatal: unable to access xxxxx OpenSSL SSL_read: Connection was reset, errno 10054

产生原因：一般是这是因为服务器的SSL证书没有经过第三方机构的签署，所以才报错

解决办法：控制台输入

`git config --[global](https://so.csdn.net/so/search?q=global&spm=1001.2101.3001.7020) http.sslVerify "false"`