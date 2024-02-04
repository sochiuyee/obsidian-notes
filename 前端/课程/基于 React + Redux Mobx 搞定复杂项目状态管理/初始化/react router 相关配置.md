#### 下载相关依赖

`npm install react-router react-router-config react-router-dom @types/react-router-config @types/react-router-dom`


```json
"react-router": "^5.2.0",
"react-router-config": "^5.1.1",
"react-router-dom": "^5.2.0",
"@types/react-router-config": "^5.0.3",
"@types/react-router-dom": "^5.1.8",
```

##### 抽离相关的路由配置文件

![](https://cdn.nlark.com/yuque/0/2023/png/32382944/1674556584885-c2638363-deb5-4449-bde1-f6ae56853f3a.png)

  

1.  配置一一对应的关系
```js
import LoginPage from '../pages/login/index';
import IndexPage from '../pages/index/index';
import App from '../App';
```

```js
const allRoutes = [
    {
        path: '/index',
        exact: false,
        title: '',
        component: IndexPage,
    },
    {
        path: '/login',
        exact: false,
        title: '',
        component: LoginPage,
    },
];
```

2.  使用HashRouter作为路由器组件
```js
import { HashRouter as Router } from 'react-router-dom';
import { renderRoutes } from 'react-router-config';
import {allRoutes} from './routes'

class AppRoute extends Component {
    render() {
        return (
            <div>
                <Router>
                    {
                            renderRoutes(allRoutes.map((item) => ({ ...item, key: item.path })))
                        }
                </Router>
            </div>
        );
    }
}

export default AppRoute;
```


3.  使用withRouter 将App组件包裹，在App组件里获取到路由相关信息：history、location、match等

> withRouter：withRouter 是一个高阶组件 HOC ，因为默认只有被 Route 包裹的组件才能获取到路由状态，如果当前非路由组件想要获取状态，那么可以通过 withRouter 包裹来获取 history、location、match 信息

[https://v5.reactrouter.com/web/api/withRouter](https://v5.reactrouter.com/web/api/withRouter)


```js
// 将router组件包裹进withRouter里，可以获取history、location、match自动注入到props里
import { withRouter } from 'react-router-dom';

import App from '../App';

const AppWrap = withRouter(App);

class AppRoute extends Component {
    render() {
        return (
            <div>
                <Router>
                    <AppWrap>
                        {
                            renderRoutes(allRoutes.map((item) => ({ ...item, key: item.path })))
                        }
                    </AppWrap>
                </Router>
            </div>
        );
    }
}

import React, { Component } from 'react';
import { RouteComponentProps } from 'react-router-dom';

// 修改App传入withRouter不是路由组件的问题
interface Props extends RouteComponentProps {}

class App extends Component<Props> {
    // 判断路径自动去首页
    handleRoute = () => {
        // App 通过withRouter包裹后，可以通过props获取到路由信息：history、location、match
        const { history, location } = this.props;
        const { pathname } = location;
        if (pathname === '/') {
            history.push('index');
            return false;
        }
        return true;
    }

    render() {
        const { children } = this.props;
        return (
            <div>
                {
                    this.handleRoute() ? children : 'other'
                }
            </div>
        );
    }
}

export default App;
```


  

4.  渲染改造后的路由组件（将App传入）
```js
import React from 'react';
import ReactDOM from 'react-dom';

// 将改造后的路由组件渲染，而不再是App组件
import RouteComponent from './routes';

import './style.scss';

ReactDOM.render(<RouteComponent />, document.getElementById('root'));
```
