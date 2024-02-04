`npm install typescript @types/react @types/react-dom`


添加typescript 配置文件
`tsc -init // 生成tsconfig.json配置文件`


修改相关的配置项

```json
{
  "module": "es2015", // 生成代码的模板标准,使用ES6
  "allowJs": true, // 允许编译器编译JS，JSX文件
  "jsx": "react",  // 指定 jsx 格式为 react
  "outDir": "./", // 指定编译后文件所在目录，此处为tsconfig.json文件所在路径的同级位置
  "rootDir": "./", // 指定输入文件的根目录，默认情况下当前的项目目录为根目录
  "noImplicitAny": true, // 当类型为any时报错
  "moduleResolution": "node", // 指定模块解析策略，node
  "baseUrl": "./", // 用于解析非绝对模块名的基本目录，相对模块不受影响
  "paths": { // 用于设置模块名称基于baseUrl的路径映射关系
    "pages/*": [
      "src/pages/*"
    ]
  },   
}
```


![[Pasted image 20230226172639.png]]

![[Pasted image 20230226172657.png]]

新增两个typescript配置项
```json
"include": [
    "src/**/*" // 指定被编译文件所在的目录
  ],
"exclude": [ // 指定不需要被编译的目录
  "node_modules",
  "config",
  "dist"
]
```
