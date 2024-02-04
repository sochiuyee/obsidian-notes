> 同域下，多窗口之间能共享localStorage，如果页面串数据，很可能就是localStorage共享导致

> [!question]
> `localStorage`既然可以，那`sessionStorage`在多窗口之间能共享状态吗？🙋


>[!summary]
>
>多窗口之间sessionStorage不可以共享状态！！！但是在某些特定场景下新开的页面会复制之前页面的sessionStorage！！

----

==根据MDN的说法：==

`sessionStorage` 属性允许你访问一个，==对应当前源==的 session `Storage` 对象。它与 `localStorage` 相似，不同之处在于 `localStorage` 里面存储的数据没有过期时间设置，而存储在 `sessionStorage` 里面的数据在页面会话结束时会被清除。

1.  页面会话在浏览器打开期间一直保持，并且==重新加载或恢复页面仍会保持原来的页面会话==。
2.  **在新标签或窗口打开一个页面时会复制顶级浏览会话的上下文作为新会话的上下文，** 这点和 session cookies 的运行方式不同。
3.  打开==多个相同的 URL== 的 Tabs 页面，==会创建各自的 `sessionStorage`==。
4.  关闭对应浏览器标签或窗口，会清除对应的 `sessionStorage`。

----
###### 实操

在百度的<span style="background:rgba(240, 200, 0, 0.2)">页面A</span>增加一个按钮，再设置session缓存
`window.sessionStorage.setItem("pageA_1","123")`

```js
var btn1 = document.getElementsByClassName('btn_wr')[0]

    var btn = document.createElement("button");

    btn.onclick = function(){

      window.open('https://www.baidu.com/s?wd=%E7%99%BE%E5%BA%A6%E7%83%AD%E6%90%9C&sa=ire_dl_gh_logo_texing&rsv_dl=igh_logo_pc')

    }

    btn1.appendChild(btn)
```

在新开的<span style="background:rgba(240, 200, 0, 0.2)">同源页面中B</span>，可以获取到刚刚的缓存
![[Pasted image 20230208115052.png]]

> [!BUG] 那之前为什么窗口不会串session？

```JS
// 在刚刚的A页面
window.sessionStorage.setItem("pageA_1","456") // (之前的pageA_1设置的值是 ‘123’ )  
window.sessionStorage.setItem("pageA_2","789")

// 在页面B尝试获取
window.sessionStorage.getItem("pageA_1") //拿到的结果还是 "123" !!!  
window.sessionStorage.getItem("pageA_2") //拿到的结果是 null !!!
```

==我们现在再次回去理解一下MDN的说法：**在该标签或窗口打开一个新页面时会复制顶级浏览会话的上下文作为新会话的上下文**==

原来只有在==本页面中以新页签或窗口打开的同源页面==会<span style="background:rgba(240, 107, 5, 0.2)">‘临时共享’</span>之前页面的sessionStorage。

而且共享这个词似乎也并不怎么准确，准确来说应该叫`复制`更加专业！
