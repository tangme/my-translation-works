## 不允许 使用 !important [Disallow !important](https://github.com/CSSLint/csslint/wiki/Disallow-%21important)

`!important`注释使用在 人为指定强调 的属性上。这往往意味着 这个待强调的特殊属性 已在整个CSS文件中失控(选择器不能正常工作),亦或 需要重构代码了。`!important`在CSS中出现的次数越多，越突显出 开发者在页面样式上的不少问题。

### 规则详情

规则 ID: `important`

此规则意在 确保代码的特指度工作正常。为此,一旦出现 `!important` 将提示警告。

以下示例将提示警告:

```css
.mybox {
    color: red !important;
}
```

