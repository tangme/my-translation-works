## 不允许 定义标题 [Disallow qualified headings](https://github.com/CSSLint/csslint/wiki/Disallow-qualified-headings)

标题元素(`h1`-`h6`) 应定义为顶级样式 且 不能在页面其它区域 定义其特定样式。标题样式 应以面向对象的思维来考虑设计，并且 在整个站点中的展示效果应当保持一直。这种方式允许在站点中复用你的样式 从而利于站点的统一展示，健壮代码与维护。举个例子，以下代码为 过度定义标题:

```css
.foo h1 {
    font-size: 110%;
}
```

### 规则说明与示例

规则 ID: `qualified-headings`

此规则意在 找出 定义了标题的规则，因此 警告将出现在  样式规则里将 标题元素 作为最后一个选择器。

以下示例 提示警告:

```css
/* qualified heading */
.box h3 {
    font-weight: normal;
}

/* qualified heading */
.item:hover h3 {
    font-weight: bold;
}
```

以下示例 不提示警告:

```css
/* Not qualified */
h3 {
    font-weight: normal;
}
```

