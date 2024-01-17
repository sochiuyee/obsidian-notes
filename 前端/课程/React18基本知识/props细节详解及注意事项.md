###### 前置知识
#class继承

```js
class Person {
  constructor(name) {
	this.name = name
  }
  getName() {
	console.log(this.name)
  }
}

class Student extends Person{
  constructor(name) {
	super(name) // super() 返回的是子类的实例，即 super 内部的 this 指向的是Student。super() 相当于 Person.prototype.constructor.call(this)
  }
  getName() {
  }
}

// 生成Student实例时，先执行子类的构造函数constructor里的内容，获取name,再执行super（此时会生成一个继承父类的this）
let p = new Student('Jack')
p.getName()
```


###### this.props在构造器中使用，需要super(props)

```js
class App{
	constructor(props) {
		super() // 在constructor里获取props需要将props传给super，但是在constructor以外的地方还是可以拿到this.props
		console.log(this.props) // undefined
	}
}

class App{
	constructor(props) {
		super(props)
		console.log(this.props) // undefined
	}
}
```

###### 多属性传递可通过扩展运算符实现
```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <!--需要引入babel才能渲染页面-->
  <script src="https://cdn.bootcdn.net/ajax/libs/babel-standalone/7.0.0-beta.3/babel.js"></script>
  <!--需要引入react相关模块-->
  <script src="https://unpkg.com/react@17/umd/react.development.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js" crossorigin></script>
</head>
<body>
  <div id="root"></div>
  <!--使用script标签里写jsx，需要给script标签加上type="text/babel"属性-->
  <script type="text/babel">
    const domNode = document.getElementById('root');
    class App extends React.Component{
      render() {
        return(
        // 通过拓展运算符传递props后，还是使用this.props.属性取值
          <div>this props {this.props.msg}</div>
        )
      }
    }
    
    let info = {
      msg: 'hi react',
      age:18
    }
    let element = (
    // 给props传递多个属性，可以使用拓展运算符
      <App {...info} />
    )
    ReactDOM.render(element, domNode)
  </script>
</body>
</html>
```

###### 单向数据流，props不能直接修改
```js
<App name="Joey" />
this.props.name = 'Jack' // props是从父组件传过来，子组件不能修改props
```

###### 给属性限定类型与添加默认值
```js
class Button extends Component {
	// 需要static defaultProps 规定默认props
	static defaultProps = {  
	color: 'blue'
};  
	render() {
		return <button className={this.props.color}>click me</button>;  
	}
}

// If the `color` prop is not provided or is `undefined`, it will be set by default to `'blue'`:
{/* this.props.color is "blue" */}  
<Button />
```
defaultProps 会在==运行时==用来弥补编译时处理不到的情况，如果用ts就可以在编译时就处理，不需要static defaultProps


###### 单独属性的值为true
```js
// 属性不写value值默认为true
<Button disabled />
```
