## 许允许空规则 [Disallow empty rules](https://github.com/CSSLint/csslint/wiki/Disallow-empty-rules)

空规则即 不包含任意属性(没有定义样式属性) ,如下:

```css
.foo {
}
```

许多时候呢，空规则的出现是因为 重构了样式而忘记了删除冗余代码造成的。消除空规则带来的结果就是 缩小了样式文件大小 和 精简了待游览器处理的样式信息。

### 规则详情

规则 ID: `empty-rules`

此规则 在CSS样式中发现为空规则时 出现警告。以下示例将会出现警告:

```css
.mybox { }

.mybox {

}

.mybox {
    /* a comment */
}
```

