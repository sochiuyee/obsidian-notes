
```json
{
  "presets": [
    "@babel/preset-env", // 用于处理ES6的语法
    "@babel/preset-react", // 用于处理react的语法
  ],
  "plugins": [
    "@babel/transform-runtime"
  ]
}
```


babel-polyfill

💭 不转换新的 API，例如Iterator、Generator、Set、Maps、Proxy、Reflect、Symbol、Promise 等全局对象，以及一些定义在全局对象上的方法（比如 Object.assign）都不会转译。如果想使用这些新的对象和方法，则需要为当前环境提供一个垫片（polyfill）。

  

babel-runtime

💭 babel-polyfill解决了Babel不转换新API的问题，但是直接在代码中插入帮助函数，会导致污染了全局环境，并且不同的代码文件中包含重复的代码，导致编译后的代码体积变大。Babel为了解决上述问题，提供了单独的包babel-runtime用以提供编译模块的工具函数

babel-plugin-transform-runtime

💭为了方便使用 babel-runtime，解决手动 require 的苦恼