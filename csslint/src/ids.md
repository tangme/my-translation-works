## 不允许 ID 选择器 [Disallow IDs in selectors](https://github.com/CSSLint/csslint/wiki/Disallow-IDs-in-selectors)

一直以来,开发者对 ID选择器 要么感情甚好 要么情有独钟。但是呢,ID选择器也多多少少有些副作用:它完全是唯一的,因此不能复用。可在你的页面中,对所有元素都使用ID选择器,但因此,你会失去CSS其它方面带来的诸多益处。

CSS的好处之一就是可在多处 复用样式规则。当你开始使用ID选择器时,就不经意间将样式局限在了单个元素上。假设你的代码如下:

```css
#header a {
    color: black;
}
```

这个样式只会在ID为`header` 下的a标签 起效。但假设现在,你想在页面中的另外一个章节也使用同样的样式,估计你只能重新再定义一个类来实现效果,如下:

```css
#header a,
.callout a {
    color: black;
}
```

一旦你明白此处的含义,你怕是只会使用类定义而不会声明ID选择器了。

```css
.callout a {
    color: black;
}
```

最终,你可能将 不在需要也不想再使用ID选择器,而使用 类选择器 取代其效果。弃用ID选择器后,你将解锁释放CSS复用的最大能力。

### 规则详情

规则 ID: `ids`

此规则意在 提示 不使用ID选择器从而提高代码复用和可维护性。任何一处的ID选择器 将提示 警告。

以下示例将 提示警告:

```css
#mybox {
    display: block;
}

.mybox #go {
    color: red;
}
```

