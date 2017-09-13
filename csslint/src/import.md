## 不允许 使用@import [Disallow @import](https://github.com/CSSLint/csslint/wiki/Disallow-%40import)

`@import`命令用于在CSS文件中 引用其它的CSS文件,例子如下:

```css
@import url(more.css);
@import url(andmore.css);

a {
    color: black;
}
```

此代码在开始位置 引用了另外两个样式表。当游览器在解析此代码时,会在每个`@import`后开始下载指定的文件,而 停止执行后面的代码。也就是说 在`@import`指定的文件未下载完成前,游览器不会同时下载其它的样式文件,总而失去了 并行下载CSS的优势。

有两种替代`@import`的方式:

1. 使用构建工具,在部署前,就将需要合并的CSS文件串联至一起。
2. 使用多个`<link>`标签来引入你需要的CSS样式。`<link>`引入是支持并行下载的。

### 规则详情

规则 ID: `import`

此规则 在使用`@import`时 提示警告。

以下示例将提示警告:

```css
@import url(foo.css);
```

