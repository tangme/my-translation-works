## 不允许 outline:none [Disallow outline:none](https://github.com/CSSLint/csslint/wiki/Disallow-outline%3Anone)

`outline`属性用于在元素的四周定义边框。不同于`border`属性,`outline`不会改变元素的大小与布局。正因如此，游览器常用`outline`来突出 激活状态的元素。当元素被选中为焦点时，在IE和火狐(Firefox)游览器中，`outline`所渲染的元素 是单像素的点状线条。

焦点轮廓，能直观的提醒用户当前页面获得焦点的元素，因此 在辅助提示上的重要性不言而喻。对于纯键盘用户而言，如果当前焦点元素没有明显的视效指明，就几乎不可能追踪到页面中所选的元素。不幸的是，默认样式下的焦点轮廓，颜值有些低，不美观，以至 在代码中将其移除了,如下:

```css
a {
    outline: none;
}
```

或

```css
a {
    outline: 0;
}
```

以上两种方式都将移除元素的外轮廓，即便在元素获得焦点时，外轮廓也不会出现。这对于 辅助提示 是不友好的。

当然，你可以给用户提供 自定义焦点效果，从而替换默认的点状边框。为此，移除掉`outline`,添加对应的改善效果，就很人性化很合理了。那么,好的解决方式之一就是使用 `:focus` 来提供新的样式 的同时，重设`outline`,例子如下:

```css
a:focus {
    border: 1px solid red;
    outline: none;
}
```

### 规则详情

规则 ID: `outline-none`

此规则意在 确保纯键盘用户 获得焦点提示。为此,规则发现以下情况 提示警告:

1. `outline: none` 或 `outline: 0` 在选择器中使用,但未指定 `:focus`
2. `outline: none` 或 `outline: 0` 在选择器中使用,虽指定`:focus`但其未定义 替换属性

以下示例将 提示警告:

```css
/* no :focus */
a {
    outline: none;
}

/* no :focus */
a {
    outline: 0;
}

/* :focus but missing a replacement treatment */
a:focus {
    outline: 0;
}
```

以下示例 不会提示警告:

```css
/* :focus with outline: 0 and provides replacement treatment */
a:focus {
    border: 1px solid red;
    outline: 0;
}
```

