## 要求备用色彩  [Require fallback colors](https://github.com/CSSLint/csslint/wiki/Require-fallback-colors)

刚开始时，有三种方式来指定颜色：使用16进制,、使用3或6位字符串、使用颜色名称 如 `red` 或 `rgb()`。但在CSS3中，新增了几种颜色定义的形式，包括 `rgba()`,`hsl()`,`hsla()`。这些新的颜色格式 显著提升了开发者使用色彩的灵活可塑性，同时使得那些老版游览器看上去更糟了。

这个规则源于 游览器的CSS解析器 会略过不识别的名称或值。像IE8或更早的这类老版游览器，不识别 `rgba()`,`hsl()`,`hsla()`,其结果就是会忽略定义的属性。请看如下代码:

```css
.box {
    background: #000;
    color: rgba(100, 100, 200, 0.5);
}
```

支持此格式的游览器将正常解析此CSS代码。但不支持的游览器，因不能解析rgba的值而完全忽略此`color`的属性。也就意味着`color`的实际值将继承至上下文环境，也可能最终值为黑色(与背景色一致)。为防止此情况，就需要使用十六进制颜色值、颜色名称或rga()格式来设定一个备用色彩，如下:

```css
.box {
    background: #000;
    color: blue;
    color: rgba(100, 100, 200, 0.5);
}
```

备用色彩 须要在 新颜色格式的前方定义，以确保 老版游览器能正常解析并使用，新版游览器也能继续执行新的颜色格式。

### 规则详情

规则 ID: `fallback-colors`

此规则 意在确保在所有的游览器上都能显示合适的颜色。为此，将在如下情形 提示警告:

1. `color`属性使用`rgba()`,`hsl()`,`hsla()`颜色值时,在前处 未使用针对老版游览器的`color`颜色格式。
2. `background`属性使用`rgba()`,`hsl()`,`hsla()`颜色值时,在前处 未使用针对老版游览器的`background`颜色格式。
3. `background-color`属性使用`rgba()`,`hsl()`,`hsla()`颜色值时,在前处 未使用针对老版游览器的`background-color`颜色格式。

以下示例将会提示警告:

```
/* missing fallback color */
.mybox {
    color: rgba(100, 200, 100, 0.5);
}

/* missing fallback color */
.mybox {
    background-color: hsla(100, 50%, 100%, 0.5);
}

/* missing fallback color */
.mybox {
    background: hsla(100, 50%, 100%, 0.5) url(foo.png);
}

/* fallback color should be before */
.mybox {
    background-color: hsl(100, 50%, 100%);
    background-color: green;
}
```

以下示例将 不会提示警告:

```css
/* fallback color before newer format */
.mybox {
    color: red;
    color: rgba(255, 0, 0, 0.5);
}
```

