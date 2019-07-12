## 不允许使用 盒子大小 [Disallow box sizing](https://github.com/CSSLint/csslint/wiki/Disallow-box-sizing)

CSS的`box-sizing`属性用来定义 边框，内边距，是如何相互影响宽度和高度的。此属性默认值为`content-box`，意思是 宽和高是由元素内容本身决定，然后 内边距与边框 再将内容包裹上。请看以下例子:

```css
.mybox {
    border: 1px solid black;
    padding: 5px;
    width: 100px;
}
```

这个盒子的实际宽度为112像素。这是因为内容将占据100像素的宽度，然后内容两侧分别加上5像素的内边距，接着两侧再加上1像素的边框。

当你将`box-sizing`的属性值改变至`border-box`时，计算方式则不同了:

```css
.mybox {
    box-sizing: border-box;
    border: 1px solid black;
    padding: 5px;
    width: 100px;
}
```

此盒子的实际宽度为100像素而其中供内容的可用空间为88像素(100-5px[左]内边距-5px[右]内边距-1px[左]边框-1px[右]边框)。大多数情况下认为`border-box`的设置更加合乎逻辑，也更像宽高属性表达的含义。

但是呢但是呢,在使用`box-sizing`时会有个小小的问题,也就是IE6 IE7是不支持`box-sizing`这个属性的。因此会展示出不同于盒子模型设置属性的效果。

### 规则详情

规则 ID: `box-sizing`

此规则在`box-sizing`属性使用时会出现警告。其含义即 提示开发者 此属性在IE6 IE7或更早期的游览器上得不到支持。

以下示例将会出现警告:

```css
.mybox {
    box-sizing: border-box;
}

.mybox {
    box-sizing: content-box;
}
```

