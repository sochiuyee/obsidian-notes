>[!tips] 自动批处理
> 批处理是 React 中对于 SetState 的合并，也就是常考常说的，为什么 react 中 setstate 并不是一个实时的动作。就是因为框架内部替你做了一个合并，以此减少渲染次数。但是 react18 之前这种合并仅限于同步代码中。如果你在任意异步任务中进行了多次的 setstate，这些行为并不会被自动合并。而 react18 对此做了优化。
> 
> 
	既然默认是自动批处理的，那么setState是一个异步方法
	批处理就是合并多个setState，提供了回调写法
	自动批处理:有助于减少在状态更改时发生的重新染次数
	在React18之前也有批处理的，但是在Promise、setTimeout原生事件中是不起作用的
	ReactDoM.flushSync可以取消批处理操作

> 例如，如果你在同一个点击事件里有两个状态更新，React总是把它们分到一个重新渲染中。如果你运行下面的代码，你会看到每次点击时，==React只执行一次渲染==，尽管你设置了两次状态

```js
function handleClick() { 
	setCount(c => c + 1); 
	setFlag(f => !f); 
	// React 只会在最后重新渲染一次（这是批处理！） 
}
```



react 18之前，自动批处理仅限于同步的setState执行，多个同名的属性，会替换最终只执行一次。
但是在异步回调里，不会执行自动批处理，多次的setState还是会执行多次
```js
// React 18之前
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <script src="https://cdn.bootcdn.net/ajax/libs/babel-standalone/7.21.4/babel.js"></script>
  <!-- <script src="https://cdn.bootcdn.net/ajax/libs/babel-standalone/7.0.0-beta.3/babel.js"></script> -->
  <script src="https://unpkg.com/react@17/umd/react.development.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js" crossorigin></script>
</head>
<body>
  <div id="root"></div>
  <script type="text/babel">
    const domNode = document.getElementById('root');
    class Button extends React.Component {
      state = {
        count: 1
      }
      handleClick = () => {
        // React18之前自动批处理仅限于同步的setState，会自动覆盖相同的属性，只打印一次渲染了
        // 页面上的state只会每次点击+1
        this.setState({
	        count: this.state.count + 1
         })
         this.setState({
           count: this.state.count + 1
         })
         this.setState({
           count: this.state.count + 1
         })


        // 在React18之前也有批处理的，但是在Promise、setTimeout原生事件中是不起作用的
        // 页面上的state只会每次点击+3，打印三次渲染了
        setTimeout(() => {
          this.setState((state) => ({
            count: state.count + 1
          }))
          this.setState((state) => ({
            count: state.count + 1
          }))
          this.setState((state) => ({
            count: state.count + 1
          }))
        })
      }

		// 使用回调函数形式收集队列进行批处理，非回调形式修改同样的属性会覆盖
		// 页面上的state只会每次点击+3，打印一次渲染了
	     this.setState((prevState, props) => {
          return {count: prevState.count + 1};
        });

        this.setState((prevState, props) => {
          return {count: prevState.count + 1};
        });
        
	    this.setState((prevState, props) => {
          return {count: prevState.count + 1};
        });

      render() {
        console.log('渲染了')
        return (
          <div>
            <button type="button" onClick={this.handleClick}>Click Me!</button>
            <div>{this.state.count}</div>
          </div>
        )
      }
    }

    let element = (
      <Button />
    )
  
    ReactDOM.render(element, domNode)
  </script>
</body>
</html>
```
![[Pasted image 20230406105330.png]]


React18 执行

```js
import { useState } from 'react'
function App() {
  const [num1, setNum1] = useState(1)
  const add = () => {
    setTimeout(() => {
      setNum1((pre) => pre + 1)
      setNum1((pre) => pre + 1)
      setNum1((pre) => pre + 1)
    })
  }
  console.log('渲染了')
  return (
    <div className="App">
      <header className="App-header">react 18</header>
      <p>num1 : {num1}</p>
      <button onClick={add}>+1</button>
    </div>
  )
}

export default App
```

![[Pasted image 20230406105803.png]]
>[!question] 为什么 react 的函数组件每次渲染执行两次?
>https://www.zhihu.com/question/387196401
是因为 React 在 Dev mode 下会刻意执行两次渲染，以防止组件内有什么 side effect 引起 bug，提前预防。