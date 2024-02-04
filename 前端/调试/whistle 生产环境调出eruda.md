[[whistle 抓包]]

加载eruda
```js
// load_eruda.js
(function() {
  var script = document.createElement('script');
  script.onload = function() {
    eruda.init();
  };
  script.src = 'https://cdn.jsdelivr.net/npm/eruda';
  document.body.appendChild(script);
})()
```
![[Pasted image 20230420143008.png]]


配置相关的域名
```js
https://mp.mhealth100.com/ jsAppend://{load_eruda.js}
https://development.mhealth100.com/ jsAppend://{load_eruda.js}
https://preproduction.mhealth100.com/ jsAppend://{load_eruda.js}
```
![[Pasted image 20230420143110.png]]