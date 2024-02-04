![[Pasted image 20230226171558.png]]
###### 具体配置
```js
"scripts": {
    "dev": "webpack server --progress --config config/webpack.dev.config.js",
    "build": "webpack --progress --config config/webpack.prod.config.js"
},
```
![[Pasted image 20230226171644.png]]
-   通过 CLI 调用 webpack-dev-server，方式是：npx webpack serve
-   --progress 在浏览器中以百分比显示编译进度
-   --config 指定打包的配置文件，一般都是分dev和build,也就是开发环境和生产环境，因为开发环境需要很多的调试信息或者其他的特殊配置来方便开发


###### HtmlWebpackPlugin 的配置
https://github.com/jantimon/html-webpack-plugin#options
![[Pasted image 20230226171750.png]]

将webpack拆分成三个文件配置

webpack.base.config.js
```js
const path = require('path')

const webpackBaseConfig = {
  entry: path.join(__dirname, '../src/index.jsx'),
  output: {
    path: path.join(__dirname, '../dist'),
    filename: '[name].[fullhash:4].js'
  },
  resolve:{
    // 导入的模块没有拓展名，就按指定的拓展名一一寻找
    extensions:['.js','.jsx']
  },
  module: {
    rules: [
      {
        test: /\.js[x]/,
        use: 'babel-loader'
      },
      {
        test: /\.(sc|c)ss/,
        // 处理sass文件
        use: ['style-loader','css-loader', 'sass-loader']
      }
    ]
  }
}

module.exports = webpackBaseConfig
```


开发环境配置:webpack.dev.config.js

```js
const path = require('path')
const webpack = require('webpack')
const { merge } = require('webpack-merge')
const OpenBrowserPlugin = require('open-browser-webpack4-plugin')
const HtmlWebpackPlugin = require('html-webpack-plugin')

const webpackConfigBase = require('./webpack.base.config')

const PORT = 8080

const webpackConfigDev = {
  mode: 'development',
  plugins: [
    new webpack.HotModuleReplacementPlugin(), // 开启热更新
    // 让index.html自动帮我们将生成的bundle添加到html中
    new HtmlWebpackPlugin({
      title: 'React App',
      filename: 'index.html', // 输出文件的文件名称
      inject: 'body', // javascript资源将被放置在body元素的底部
      template: path.join(__dirname, '../src/index.html') // 模板的Webpack相对路径或绝对路径
    }),
    new OpenBrowserPlugin({
      url: `http://localhost:${PORT}/#/`
    })
  ],
  devtool: 'eval-source-map' // 定位到错误在原代码的位置，不会产生单独的文件，但是可以显示行和列
}

module.exports = merge(webpackConfigBase, webpackConfigDev)
```


生产环境的配置:webpack.prod.config.js

```js
const path = require('path')
const { merge } = require('webpack-merge')
const HtmlWebpackPlugin = require('html-webpack-plugin')

const webpackConfigBase = require('./webpack.base.config')
const { CleanWebpackPlugin } = require('clean-webpack-plugin')

const webpackConfigProd = {
  mode: 'production',
  plugins: [
    new CleanWebpackPlugin(), // 每次打包前清除dist里面的内容
    new HtmlWebpackPlugin({
      title: 'React App',
      filename: 'index.html', // 输出文件的文件名称
      inject: 'body', // javascript资源将被放置在body元素的底部
      template: path.join(__dirname, '../src/index.html') // 模板的Webpack相对路径或绝对路径
    })
  ]
}

module.exports = merge(webpackConfigBase, webpackConfigProd)
```
