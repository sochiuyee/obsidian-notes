###### 认识视口
在前面我们已经简单了解过视口的概念了
- 在一个浏览器中，我们可以看到的区域就是视口 (viewport) ;
- 我们说过fixed就是相对于视口来进行定位的;
==在PC端的页面中==，我们是不需要对视口进行区分，因为我们的==布局视口和视觉视口是同一个==

但是在移动端，不太一样，你布局的视口和你可见的视口是不太一样的。
- 所以在默认情况下，移动端的布局视口是大于视觉视口的;
所以在移动端，我们可以将视口划分为三种情况:
1. 布局视口 (layout viewport)
2. 视觉视口 (visuallayout)
3. 理想视口 (ideallayout)

###### 移动端
==默认情况下，布局视口的宽度是980px==
![[Pasted image 20230319180215.png]]


![[78a634fdbf14a332594541c14c1399e.jpg]]

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <!-- <meta name="viewport" content="width=device-width, initial-scale=1.0"> -->
  <title>Document</title>
  <style>
    .box {
      width:100px;
      height: 100px;
      background: pink;
    }
  </style>
</head>
<body>
  <div class="box"></div>
</body>
</html>
```
![[Pasted image 20230319181120.png]]
虽然在浏览器上显示高度是100×100，但是因为布局视口是980px，元素的布局是基于布局视口的980px展示100px，但是视觉视口是375px，所以元素会按一定比例缩放

如果想在375px的视觉视口上展示100px的元素，需要修改meta标签的content

`<meta name="viewport" content="width=375px">`

![[Pasted image 20230319182045.png]]

###### 修改meta标签达到自适应
想在不同的设备上展示基于视口布局的100px元素，需要修改meta标签的content为设备宽度
`<meta name="viewport" content="width=device-width>`

| 属性名        | 取值                  | 描述                                 |
| ------------- | --------------------- | ------------------------------------ |
| width         | 正整数或device-width  | 定义视口的宽度，单位为像素           |
| height        | 正整数或device-height | 定义视口的高度，单位为像素，一般不用 |
| initial-scale | [0.0-10.0]  | 定义初始缩放值                       |
| minimum-scale | [0.0-10.0]  | 定义放大最大比例，它必须小于或等于maximum-scale设置 |
| maximum-scale | [0.0-10.0] | 定义缩小最小比例，它必须大于或等于minimum-scale设置 |
| user-scalable	| yes/no | 定义是否允许用户手动缩放页面，默认值 yes |

💗 ==meta标签可以设置html不缓存==

```html
<meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate" />
<meta http-equiv="Pragma" content="no-cache" />
<meta http-equiv="Expires" content="0" />
```


---

###### rem 布局
1. 设置meta标签为设备宽度，设置不允许缩放，最大最小缩放比例为1.0
	1. `<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">`
2. 设置html标签的font-size大小
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <title>Document</title>
  <style>
    body {
	  /*
	  * html: 1rem = 37.5px
	  * body 通常设置16px,换算 1rem/37.5px = x / 16px
	  */
      font-size: 0.427rem;
    }
    .box {
      width:2.667rem;
      height: 2.667rem;
      background: pink;
    }

  </style>
</head>
<body>
  <script>
    (
      function (doc, win) {
        var docEl = doc.documentElement,
        resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
        recalc = function() {
          var clientWidth = docEl.clientWidth
          // 设置html标签的font-size为设备宽度的1/10
          docEl.style.fontSize = (clientWidth / 10) + 'px'
        }
        // 屏幕旋转或窗口缩放
        win.addEventListener(resizeEvt, recalc, false)
        // 首次加载
        win.addEventListener('DOMContentLoaded', recalc, false)
      }
    )(document, window)
  </script>
  <div class="box">
    <p>哈哈</p>
  </div>
</body>
</html>
```

1. 设备body标签font-size大小
	1. 不设置的话，字体默认是html的字体大小

vscode 可以使用px to rem插件自动转换rem单位

webpack可以使用插件
`npm install px2rem-loader -D --save`

```js
// 配置webpack loader
var px2remLoader = {
	loader: 'px2rem-loader',
	options: {
		remUnit: 75
	}
}
```
