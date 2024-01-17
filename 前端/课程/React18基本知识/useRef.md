> react中创建ref的几种方式：
> React.createRef() ＆「回調函數ref」＆「useRef」。 其中React.createRef 和 callback ref 不可以在函數組件中使用，因爲函數組件沒有實例


### createRef()

使用 `React.createRef()` 创建的，并通过 `ref` 属性附加到 React 元素。在构造组件时，通常将 Refs 分配给实例属性，以便可以在整个组件中引用它们

```jsx
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <script src="<https://cdn.bootcdn.net/ajax/libs/babel-standalone/7.21.4/babel.js>"></script>
  <!-- <script src="<https://cdn.bootcdn.net/ajax/libs/babel-standalone/7.0.0-beta.3/babel.js>"></script> -->
  <script src="<https://unpkg.com/react@17/umd/react.development.js>" crossorigin></script>
  <script src="<https://unpkg.com/react-dom@17/umd/react-dom.development.js>" crossorigin></script>
</head>
<body>
  <div id="root"></div>

  <script type="text/babel">
    const domNode = document.getElementById('root');

    class MyComponent extends React.Component {
      constructor() {
        super()
        this.myRef = React.createRef() // 使用React.createRef创建ref
      }

      handleClick() {
        this.myRef.current.focus()
      }

      render() {
        return(
          <div>
            <button onClick={() => this.handleClick()}>click me!</button>
            <input ref={this.myRef}/> // 通过 ref 属性附加到 React 元素
          </div>
        )
      }
    }

    let element = (
      <MyComponent />
    )

    ReactDOM.render(element, domNode)
  </script>
</body>
</html>
```

### callback Ref

```jsx
<div id="root"></div>
  <script type="text/babel">
    const domNode = document.getElementById('root');
    class MyComponent extends React.Component {

      componentDidMount() {
        console.log('ref---', this.myRef)
        this.myRef.focus()
      }

      render() {
        return(
          <div>
            <input ref={(ele) => { // ref属性传入一个回调函数
              this.myRef = ele
            }}/>
          </div>
        )
      }
    }

    let element = (
      <MyComponent />
    )

    ReactDOM.render(element, domNode)
  </script>
```

---

💭 React.createRef 和 callbackRef**不能在函数组件上使用： 因为函数组件没有this实例**

> 如果要在函数组件中使用 ref：
> 
> -   可以将该组件转化为 class 组件
> -   可以使用 forwardRef（可与 useImperativeHandle 结合使用）
> -   在函数组件 使用`useRef` </aside>

### 使用 forwardRef达到refs转发

💡 `React.forwardRef(render)`的返回值是`react`组件，接收的参数是一个 `render`函数，函数签名为`render(props, ref)`，第二个参数将其接受的 [ref]属性**转发**到`render`返回的组件中。

```jsx
// MyInput.jsx
import { forwardRef } from 'react';

const MyInput = forwardRef(function MyInput(props, ref) {
  const { label, ...otherProps } = props;
  return (
    <label>
      {label}
      <input ref={ref} {...otherProps} />
    </label>
  );
});
  
export default MyInput
```

```jsx
// App.jsx
import { useRef } from 'react';
import MyInput from './MyInput.js';

export default function Form() {
  const ref = useRef(null);

  function handleClick() {
    ref.current.focus();
  }

  return (
    <form>
      <MyInput label="Enter your name:" ref={ref} />
      <button type="button" onClick={handleClick}>
        Edit
      </button>
    </form>
  );
}
```

1.  当 `ref` 属性用于 HTML 元素时，接收底层 DOM 元素作为其 `current` 属性。
2.  当 `ref` 属性用于自定义 class 组件时，`ref` 接收组件实例作为其 `current` 属性。
