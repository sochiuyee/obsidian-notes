https://help.obsidian.md/How+to/Use+callouts

启用callout模块: > https://www.zhihu.com/question/387196401

==其中INFO 可替换成其他==

==默认有12种风格==。每一种有不同的颜色和图标。

==只要把上面例子里的 INFO 替换为下面任意一个就行。==

```js
note
abstract, summary, tldr
info, todo
tip, hint, important
success, check, done
question, help, faq
warning, caution, attention
failure, fail, missing
danger, error
bug
example
quote, cite
```

###### 自定义标题，然后直接不要主体部分
`> [!TIP] 需要展示的内容`

###### 折叠
可以使用 `+` 默认展开或者 `-` 默认折叠正文部分

```js
[!FAQ]- Are callouts foldable? > Yes! In a foldable callout, the contents are hidden until it is expanded.

```

###### 自定义样式
Callouts的类型和图标是用CSS来描述，颜色是r, g, b 三色组，图标有相应的 icon ID (比如lucide-info)。也可以自定义SVG图标。
```css
.callout[data-callout="my-callout-type"] {
    --callout-color: 0, 0, 0;
    --callout-icon: icon-id;
    --calout-icon: '<svg>...custom svg...</svg>';
}
```
