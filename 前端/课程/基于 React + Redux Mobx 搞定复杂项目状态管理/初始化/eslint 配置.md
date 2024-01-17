### 配置eslint
```json
// 配置Airbnb校验规则及其依赖
"eslint": "^7.30.0",
"eslint-config-airbnb": "^18.2.1",
"eslint-plugin-import": "^2.23.4",
"eslint-plugin-jsx-a11y": "^6.4.1",
"eslint-plugin-react": "^7.24.0",
"eslint-plugin-react-hooks": "^4.2.0",
```


### 在根目录新建.eslintlrc.json并配置
```json
{
  "env": {
    "browser": true // 在浏览器环境运行
  },
  "extends": ["airbnb"], // 使用爱彼迎的校验规则，前提是安装相关的依赖
  "rules": {
    "indent": ["error", 4], // 使用4个空格才不报错
    "react/jsx-indent": ["error", 4],
    "react/prefer-stateless-function": "off" // 关掉相关的校验规则，比如这里规定要用纯函数去编写react，但是想继续用class，就要关闭这个规则
  }
}
```


### 安装typescript的eslint依赖

`npm install @typescript-eslint/eslint-plugin@^4.28.2 @typescript-eslint/parser@^4.28.2`
```json
"rules": {
  "react/jsx-filename-extension": ["error", { // 支持在 .js、jsx、ts、tsx 文件中支持使用 JSX 语法
    "extensions": [".js", ".jsx", ".ts", ".tsx"]
  }],
  "no-unused-vars": "warn", // 没有使用的变量，报警告
  "no-use-before-define": "off" // 关闭禁止定义前使用
}
```


### webpack解析不了.tsx文件，需要安装相关的依赖去解析

![[Pasted image 20230226172240.png]]

`npm install ts-loader@^9.2.3 --save-dev`

添加解析ts文件的ts-loader配置

```json
module: {
  rules: [
    // 添加解析ts文件
    {
      test: /\.ts[x]/,
      use: 'ts-loader',
    },
  ]
}
```

![[Pasted image 20230226172419.png]]

###### 配置alias报eslint unable to find module xxx
[[前端工程开发代码工具库配置]]