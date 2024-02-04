[vue debug on vscode](https://v2.cn.vuejs.org/v2/cookbook/debugging-in-vscode.html)
1. 在vue的配置文件加上生成source map的配置

```js
devtool: 'source-map', // cli2配置

// vue cli3配置
module.exports = {  
	configureWebpack: {  
	devtool: 'source-map'  
	}  
}
```

1. 配置vscode的launch.json

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "pwa-chrome",
      "request": "launch",
      "name": "vuejs: chrome",
      "url": "http://localhost:8081", // 修改为实际的启动服务的url
      "webRoot": "${workspaceFolder}/src",
      "breakOnLoad": true,
      "sourceMapPathOverrides": {
        "webpack:///src/*": "${webRoot}/*"
      }
    }
  ]
}
```

3. 在vscode中打断点
