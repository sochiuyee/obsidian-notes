> ==视口布局的优点：宽度和高度全部自动适应==！再加上rem布局的字体适应，可以完美解决各种屏幕适配问题！

###### vw、vh是基于视口的布局方案，故这个meta元素的视口必须声明。（解决宽高自动适配）
`<meta name="viewport" content="width=device-width,inital-scale=1.0"/>`

###### rem布局-解决字体适配
```css
/*常见的屏幕尺寸1920和1366（14吋屏幕），将屏幕分成100份*/
1920 * 100 = 19.2 // 1rem = 19.2px
1366 * 100 = 19.2 // 1rem = 13.66px

html{ 
	font-size:19.20px; /*默认以设计稿为基准*/ 
}

@media only screen and (max-width: 1366px) {
	html{
		font-size:13.66px; 
	}
}
```

**vw表示1%的屏幕宽度**
750px 对应100vw
7.5px 对应1vm
1px 对应 0.1333333333333333vm

具体使用
宽高可以用vh，vw的单位，font-size使用rem布局

---

###### flexible布局方案
动态设置html的font-size
根据不同设备添加不同的data-dpr值
设置meta标签的scale为 1/dpr
将css的单位换成是rem