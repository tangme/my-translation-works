## 小心使用盒子模型大小 [Beware of box model size](https://github.com/CSSLint/csslint/wiki/Beware-of-box-model-size)

盒子模型是CSS当中最常误解的内容之一。"盒子模型 (Box model)"会参考一系列盒子属性来最终确定元素的显示。盒子的最里层为 内容。内容被内边距包裹,内边距之外再由边框包裹。盒子最终的宽度也就由以上的属性相互影响,是不是有些小困惑。来,看下面的例子:

```css
.mybox {
    border: 1px solid black;
    padding: 5px;
    width: 100px;
}
```

新手可能会觉得拥有`mybox`类的元素宽度为100像素。但实际上呢,宽度是112像素,这是因为宽度最终由 内容 内边距 边框相加而得。当开发人考虑到以上属性组合时,也会因为不同的想法行为产生错误。

通过将`box-sizing`属性值设置为`border-box`,可以使绝大多数游览器(现代游览器)遵循 宽高是 元素本身的大小,例子如下:

```css
.mybox {
    box-sizing: border-box;
    border: 1px solid black;
    padding: 5px;
    width: 100px;
}
```

那么现在,这个拥有`mybox`类的元素,实际宽度就为100像素了,内边距与边框 将占据其中的空间,剩下的88像素将是内容的宽度.

### 规则详情

规则 ID: `box-model`

此规则 意在消除潜在的盒子模型大小问题。因此,规则将在以下情况出现警告:

1.`width`被与`border`,`border-left`,`border-right`,`padding`,`padding-left`,`padding-right`属性同时使用时

2.`height`被与`border`,`border-top`,`border-bottom`,`padding`,`padding-top`,`padding-bottom`属性同时使用时

如果`box-sizing`属性已指定,则假定你已非常清楚盒子模型的规则,以上的情况,此规则将不会出现警告。

以下的例子将会出现警告:

```css
/* width and border */
.mybox {
    border: 1px solid black;
    width: 100px;
}
```

以下的例子将 不会 出现警告:

```css
/* width and border with box-sizing */
.mybox {
    box-sizing: border-box;
    border: 1px solid black;
    width: 100px;
}

/* width and border-top */
.mybox {
    border-top: 1px solid black;
    width: 100px;
}

/* height and border-top of none */
.mybox {
    border-top: none;
    height: 100px;
}
```

