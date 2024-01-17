 >[!question] 💭为什么JS和CSS文件要做打包分离？
 >1.  减少单个文件的体积，进而提升浏览加载速度
 >2.  相互独立修改，互补影响
 >	1. 各自修改代码，假如只需修改JS，那么css打包的版本不发生变化，在用户端可以使用本地css缓存
 >3.  css文件放在index.html文件的顶部，让浏览器优先解析css


安装mini-css-extract-plugin
`npm install mini-css-extract-plugin@^2.1.0 --save-dev`

##### 设置环境变量

[https://www.cnblogs.com/fe-linjin/p/11963765.html](https://www.cnblogs.com/fe-linjin/p/11963765.html)

1. 下载cross-env 依赖解决不同平台设置环境变量的问题
`npm install --save-dev cross-env`

2. 在package.json注入环境变量值
>[!INFO]
>#### process对象提供一系列属性，用于返回系统信息。
>process.env：返回一个对象，成员为当前Shell的环境变量
>### process.env.NODE_ENV的作用
>这个变量并不是 process.env 直接就有的，而是通过设置得到的。
>以webpack的工程为例，通常是运行脚本时来做这件事，例如package.json中的脚本：

```JSON
// 给env注入NODE_ENV的值
// cross-env 解决windows注入报错问题
// NODE_ENV=development 注入环境变量
"scripts": {
    "dev": "cross-env NODE_ENV=development webpack serve --progress --config config/webpack.dev.config.js",
    "build": "cross-env NODE_ENV=production webpack --progress --config config/webpack.prod.config.js"
  }
```


###### 配置webpack，区分开发环境和生产环境

生产环境使用mini-css-extract-plugin的loader解析css文件

开发环境使用style loader解析css文件

1.  配置生产环境的webpack文件（webpack.prod.config.js）

```js
const webpackConfigProd = {
    mode: 'production',
    plugins: [
        new CleanWebpackPlugin(), // 每次打包前清除dist里面的内容
        // 配置的地方应该放在打包输出html前面，因为需要那到已经输出的css文件名
        new MiniCssExtractPlugin({
            filename: '[name].[fullhash:4].css',
        }),
        new HtmlWebpackPlugin({
            title: 'React App',
            filename: 'index.html', // 输出文件的文件名称
            inject: 'body', // javascript资源将被放置在body元素的底部
            template: path.join(__dirname, '../src/index.html'), // 模板的Webpack相对路径或绝对路径
        }),
    ],
};
```

2.  在base webpack文件使用MiniCssExtractPlugin解析css文件
```js
// 获取环境变量
const devMode = process.env.NODE_ENV !== 'production';
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

// 处理css或scss文件的loader
{
    test: /\.(sc|c)ss/,
    // 处理sass文件
    use: [
        devMode ? 'style-loader' : MiniCssExtractPlugin.loader,
        'css-loader',
        'sass-loader',
    ],
}
```
