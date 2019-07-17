## 不允许 文本负缩进 [Disallow negative text indent](https://github.com/CSSLint/csslint/wiki/Disallow-negative-text-indent)

文本负缩进通常当作辅助的目的，来隐藏在屏幕上的文字。使用场景之一就是作为图像替换技术，使用文本负缩进，可确保屏幕阅读器在文本没有显示在屏幕中时也能读取其数据。使用`visibility:hidden`或`display:none`会使得屏幕阅读器略过文本信息，因此，运用文本负缩进被视为更好的辅助处理方式。

此技巧通常使用很大的负单位数值，如`-999px`或`-9999px`，如下:

```css
.mybox {
    background: url(bg.png) no-repeat;
    text-indent: -9999px;
}
```

此带有技巧性的缩进允许 背景图片展示给普通游览用户的同时，也确保了屏幕阅读器能顺利解析内联的文本信息。

当文本负缩进使用在横向视图页面时，会引起一定的麻烦，因为会出现一个很长的横向滚动条。此问题可以通过添加`direction:ltr`来解决，如下:

```css
.mybox {
    background: url(bg.png) no-repeat;
    direction: ltr;
    text-indent: -9999px;
}
```

关于文本负缩进是否会影响页面搜索排名，出现了各种不同的声音。 [Anecdotal accounts ](http://luigimontanez.com/2010/stop-using-text-indent-css-trick/) 觉得Google会把文本负缩进当作垃圾广告技术来处理，但是这并未得到验证。

### 规则说明与示例

规则 ID: `text-indent`

此规则意在 找出CSS代码中使用`text-indent`的潜在问题。警告出现在 `text-indent`的值为`-99`或类似(如，`-100`，`-999`)，而没有使用`direction:ltr`时。数值的单位不会考虑在其中，因为`px`，`em`或其它单位 会看作等同。

以下示例 提示警告:

```css
/* missing direction */
.mybox {
    text-indent: -999px;
}

/* missing direction */
.mybox {
    text-indent: -999em;
}

/* direction is rtl */
.mybox {
    direction: rtl;
    text-indent: -999em;
}
```

以下示例 不会提示警告:

```css
/* direction used */
.mybox {
    direction: ltr;
    text-indent: -999em;
}

/* Not obviously used to hide text */
.mybox {
    text-indent: -1em;
}
```

