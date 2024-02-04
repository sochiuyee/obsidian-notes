> react.development.js / react 模块     ---->    生成虚拟DOM
> react-dom.development.js (不用脚手架node下载，使用script标签引入方式，可以生成虚拟DOM)


react-dom.development.js 或 react-dom/client 模块  ---->  进行Diff算法和处理真实DOM

###### 通过script标签引入react
https://react.bootcss.com/learn/add-react-to-a-website
https://react.dev/reference/react/createElement


```html
<body>
  <div id="root"></div>
  // 生成虚拟dom
  <script src="./react.development.js"></script>
  // 进行diff算法和处理真实dom
  <script src="./react-dom.development.js"></script>
  <script>
    // react 元素 虚拟dom，不使用jsx，每创建一个元素都需要使用createElement
    const element = React.createElement('span', null, 'hello', React.createElement('span', null, 'react'))
    const domNode = document.getElementById('root');
    // 处理真实dom
    ReactDOM.render(element, domNode)
  </script>
</body>
```
