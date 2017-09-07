## 使用内核前缀 [Require compatible vendor prefixes](https://github.com/CSSLint/csslint/wiki/Require-compatible-vendor-prefixes)

实验性的CSS属性,通常需要添加内核前缀,方能实现其效果。当然,等到标准的最终统一与建立就不需要再添加前缀了。许多CSS3属性对应都有多种前缀,包括 Firefox(`-moz`),Safari/Chrome(`-webkit`),Opera(`-o`),和 Internet Explorer(`-ms`)。正因为如此，我们在使用新属性时就很容易忘记 添加属性的内核前缀。

以下属性建议追加多内核前缀:

- `animation`
- `animation-delay`
- `animation-direction`
- `animation-duration`
- `animation-fill-mode`
- `animation-iteration-count`
- `animation-name`
- `animation-play-state`
- `animation-timing-function`
- `appearance`
- `border-end`
- `border-end-color`
- `border-end-style`
- `border-end-width`
- `border-image`
- `border-radius`
- `border-start`
- `border-start-color`
- `border-start-style`
- `border-start-width`
- `box-align`
- `box-direction`
- `box-flex`
- `box-lines`
- `box-ordinal-group`
- `box-orient`
- `box-pack`
- `box-sizing`
- `box-shadow`
- `column-count`
- `column-gap`
- `column-rule`
- `column-rule-color`
- `column-rule-style`
- `column-rule-width`
- `column-width`
- `hyphens`
- `line-break`
- `margin-end`
- `margin-start`
- `marquee-speed`
- `marquee-style`
- `padding-end`
- `padding-start`
- `tab-size`
- `text-size-adjust`
- `transform`
- `transform-origin`
- `transition`
- `transition-delay`
- `transition-duration`
- `transition-property`
- `transition-timing-function`
- `user-modify`
- `user-select`
- `word-break`
- `writing-mode`

如果想让你的CSS效果跨游览器支持,那么给所有支持新属性效果的游览器增加对应的内核前缀就非常重要了。

### 规则详情

规则 ID: `compatible-vendor-prefixes`

此规则将在 缺失内核前缀的属性时 出现警告。支持的属性已在上方列表中罗列。

以下示例将会出现警告:

```css
/* Missing -moz, -ms, and -o */
.mybox {
    -webkit-transform: translate(50px, 100px);
}

/* Missing -webkit */
.mybox {
    -moz-border-radius: 5px;
}
```

