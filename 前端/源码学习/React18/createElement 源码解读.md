https://juejin.cn/post/7160981608885927972

`<div id="foo">bar</div>
```javascript
// babel转译
React.createElement("div", {id: "foo"}, "bar");
```
`
`createElement` 的第一个参数是元素类型，第二个参数是元素属性，第三个参数是子元素

###### createElement 源码所在地方
1. `pacakges/react/index.js` 文件，可以看到 `createElement` 的定义在 `./src/React` 文件
2. `export {createElement} from './src/React'; 发现是./ReactElement中暴露
3. `./ReactElement.js`文件，在这里终于找到<font color="#ffff00">最终的定义</font>
`
##### 源码分析
```javascript
/*
* 1. type代表类型，可以是标签，也可以是React组件
* 2. config代表传入的属性
* 3. children代表传入的子元素
*/
export function createElement(type, config, children) {}
```

第一段代码：对 key、ref、self、source 单独处理
```javascript
  let key = null;
  let ref = null;
  let self = null;
  let source = null;

  if (config != null) {
    if (hasValidRef(config)) {
      ref = config.ref;

      if (__DEV__) {
        warnIfStringRefCannotBeAutoConverted(config);
      }
    }

    if (hasValidKey(config)) {
      if (__DEV__) {
        checkKeyStringCoercion(config.key);
      }
      key = '' + config.key;
    }

    self = config.__self === undefined ? null : config.__self;
    source = config.__source === undefined ? null : config.__source;
```
