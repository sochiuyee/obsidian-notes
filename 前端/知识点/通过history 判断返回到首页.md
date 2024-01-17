
```js
window.history.length // 得知进入过多少个页面，但是这个length不会随后退而减少

window.history.state // 当值为null时，返回到第一页

// 监听页面的回退事件
window.addEventListener('popstate', e => {
	e.state // null的时候回到第一页
})

window.location.href
window.history.back()
window.location.href // 获取href是同步的操作，就算放在后退代码后面，前后两次获取的href都是一样
```

###### 单点登录返回

需求：从页面a单点登录跳至页面b,在页面b里做判断符合条件后location.href至c页面

问题：在页面c中点击返回按钮页面回到了a,正常情况下应该回到页面b

原因：在当前页面的 `onload` 事件发起之前，`location.href` 也是替换当前历史记录，但我是写在window.onload里的啊，不知道为什么也不行，打印history确实只有两条记录。

解决：

```js
// pushState,手动添加一条记录
history.pushState(null,null,'b.html')
window.location.href = '/c.html'
```
