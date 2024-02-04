> em单位是基于本元素或父元素font-size大小

```css
.box {
	font-size:16px;
	width:100px;
	height:100px;
	background:pink;
	border:2em blue solid; /*boder宽度是32*/
}

.box1 {
	font-size:2em; /*找box1的父元素的font-size*/
	width:100px;
	height:100px;
	background:pink;
	border:2em blue solid; /*boder宽度是32*/
}
```

###### rem
> rem 是基于==html==的font-size的em
> 针对不同设备修改html的font-size就可达到适配

```css
html {
	font-size:20px;
}

.content {
	font-size:10px;
}

.box {
	width:100px;
	height:100px;
	background:pink;
	border:2rem blue solid; /*boder宽度是40*/
}

<div class="content">
	<div class="box"></div>
</div>
```

使用vw单位动态设置html的font-size
以iPhone6 375px为例，视口是分为100vw，把375分成100的比例等于将视口也分成对应的比例（方便针对ui图的px直接÷100就是rem单位）
$$
\frac{100}{375} = \frac{x}{100}
$$
x = 26.66667


```css
html {
	font-size:26.66667vw;
}

.box {
	width:1rem;
	height:1rem;
}

/*需要重置body的font-size，否则会影响文字的大小*/
body {
	font-size: 0.16rem; /*默认重置16px大小，但是要适应不同环境，需要换成rem*/
}
```

---

蓝湖设计稿
以iPhone6为例，宽度为375px，2倍屏幕，上传到蓝湖的设计稿是web（750px），自动将像素÷2
![[Pasted image 20230319175603.png]]
![[Pasted image 20230319175718.png]]

蓝湖的375px的图就直接使用不需要÷2