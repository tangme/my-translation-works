## 要求 游览器前缀属性与标准属性 组合使用 [Require standard property with vendor prefix](https://github.com/CSSLint/csslint/wiki/Require-standard-property-with-vendor-prefix)

游览器前缀属性是 各游览器提供商在标准样式还未建成时,提供实验性 新增CSS功能,而创建的。其允许开发者和游览器提供商在之后 新增属性还未确定定稿时,发现潜在的缺陷和跨游览器兼容性问题。标准版属性通常(但也不总是)与游览器前缀版,有着相同的名字和语构,如果有两种或以上相同的游览器前缀属性 语构相似,则标准版属性与其语构保持一致。

当使用游览器前缀属性 如`-moz-border-radius`,你应当同时编写标准属性,以保障今后的兼容性。标准属性编写应在 游览器前缀属性之后,以确保 标准属性能被游览器识别使用到,如下:

```css
.mybox {
    -moz-border-radius: 5px;
    border-radius: 5px;
}
```

将标准属性放置游览器前缀属性之后 是确保一旦标准属性完全实行时,你的CSS代码能正常运转的最好方式(接着,你就可找个喝茶的时间,把以往的游览器前缀属性给删除)。

### 规则详情

规则 ID: `vendor-prefix`

此规则意在确保 不论何时使用游览器前缀属性时,与其匹配的标准属性均同时编码。因此,规则在以下条件时,提示警告:

1. 游览器前缀属性之后,没有跟随与其匹配的标准属性。
2. 与游览器前缀属性匹配的标准属性,出现在前缀属性之前。

以下示例 提示警告:

```css
/* missing standard property */
.mybox {
    -moz-border-radius: 5px;
}

/* standard property should come after vendor-prefixed property */
.mybox {
    border-radius: 5px;
    -webkit-border-radius: 5px;
}
```

以下示例 不提示警告:

```css
/* both vendor-prefix and standard property */
.mybox {
    -moz-border-radius: 5px;
    border-radius: 5px;
}
```

