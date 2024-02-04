
值没改变但是重新触发render，耗费性能



shouldcomponentupdate默认返回true，不管setstate有没有改变，都会render


不能直接修改state，这样会破坏纯组件，认为它没变不能渲染视图，需要用拓展运算符方式
不可变数据集合
