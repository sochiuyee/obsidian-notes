两种写法:React.createRef() callbackRef()
![[Screenshot_2023-04-11-23-50-20-423_com.estrongs.android.pop.png]]
梗推荐第一种，第二种可以在初始化的时候获取原生dom的场景使用
.current 获取的是原生dom

element获取的就是原生dom
![[Screenshot_2023-04-11-23-52-59-757_com.estrongs.android.pop.png]]

Refs操类组件，得到组件实例对象
![[Screenshot_2023-04-11-23-58-28-537_com.estrongs.android.pop.png]]
在组件中 ref=

Refs在类组件的转发
将创建好的createRef以props的形式传递给子组件，子组件中ref=接收的props的ref