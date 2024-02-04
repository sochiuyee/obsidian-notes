1. 在项目的根目录新建.vscode文件夹，里面配置launch.json文件

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "pwa-chrome",
      "request": "launch",
      "name": "Launch Chrome against localhost",
      "url": "http://localhost:3000", // 需要换成启动服务的端口
      "webRoot": "${workspaceFolder}"
    }
  ]
}
```

打断点
2. 在未点击断点，右键，选择添加记录点，可以断点打印
`{ 需要打印的值 } // 可以在前面加一些文字描述，id的值为：{id}`

###### debug 按钮
按钮1：运行/继续 `F5`，真正的一步一步运行
按钮2：单步跳过(又叫逐过程) `F10`，按语句单步执行。当有函数时，==不会进入函数==。  
按钮3：单步调试（又叫逐语句） `F11`：当有函数时，点击这个按钮，会==进入这个函数内==。  
按钮4：单步跳出 `⇧F11`:如果有循环，点击该按钮，会执行到循环外面的语句。  
按钮5：重启 ⇧⌘F5：  
按钮5：停止 ⇧F5：

