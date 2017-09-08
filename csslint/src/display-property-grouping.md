## 要求给display设置匹配的组合属性 [Require properties appropriate for display](https://github.com/CSSLint/csslint/wiki/Require-properties-appropriate-for-display)

只要你开心,你可以在CSS中定义任意的组合规则,但是呢,其中有些规则会因为 元素设置了`display`属性而忽略你所设置的规则。这会导致你的CSS文件中出现脏代码,同时 误解了规则理应如何运转的。

当 `display:inline`时, `width`,`height`,`margin-top`,`margin-bottom`,和`float`属性的设置 将不会起到作用,因为 内联(inline)元素不是一个盒子模型,也就无从设置这些属性。而 `margin-left`和`margin-right`依旧能起效是为了保证 缩进 的目的,其它的外边距(margin) 设置则起不到效果。`float`属性有时会用作修复 [IE6 double-margin bug](http://www.positioniseverything.net/explorer/doubled-margin.html).

其它基于`display`的情形有:

*  `display:inline-block` 不应与 `float` 同时使用。
*  `display:block` 不应与 `vertical-align` 同时使用。
*  `display:table-*` 不应与 `margin' 或 `float` 同时使用。

移除这些会被忽略或有问题的属性,能减小文件体积从而改善性能。

### 规则详情

规则 ID: `display-property-grouping`

此规则 将标识出 与`display`属性同时使用 而不起效的属性。其目的是使CSS文件更精简,更清晰而无多余代码。那么,检测出以下代码时,提示警告:

-  `display:inline` 与 `width`,`height`,`margin`,`margin-top`,`margin-bottom`,`float `。
-  `display:inline-block` 与 `float` 同时使用。
-  `display:block` 与 `vertical-align` 同时使用。
-  `display:table-*` 与 `margin' 或 `float` 同时使用。


以下示例将提示警告:

```css
/* inline with height */
.mybox {
    display: inline;
    height: 25px;
}

/* inline-block with float */
.mybox {
    display: inline-block;
    float: left;
}

/* table-cell and margin */
.mybox {
    display: table-cell;
    margin: 10px;
}
```

以下示例将 不会 提示警告:

```css
/* inline with margin-left */
.mybox {
    display: inline;
    margin-left: 10px;
}

/* table and margin */
.mybox {
    display: table;
    margin-bottom: 10px;
}
```

