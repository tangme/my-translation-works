## 不允许 星号前缀 [Disallow star hack](https://github.com/CSSLint/csslint/wiki/Disallow-star-hack)

星号前缀是有名(也可能无名)的技巧，仅用来在IE8以前的版本上指定CSS属性。通过在属性名前加上星号，老版IE游览器解析时，将当此星号不存在，而其它游览器则直接忽略此属性。例子如下:

```css
.mybox {
    border: 1px solid black;
    padding: 5px;
    width: 100px;
    *width: 200px;
}
```

在此示例中，IE7及更早版本会将`*width`属性当作`width`解析，因此实际值为`200px`；其它游览器则忽略跳过此属性，使用的实际值为`100px`。

星号前缀是依赖老版IE的CSS解析器缺陷，也因此，并不建议使用它。

### 规则说明与示例

规则 ID: `star-property-hack`

此规则意在 消除在CSS中使用星号前缀.因此,在发现属性名前使用星号时提示警告。

以下示例 提示警告:

```css
.mybox {
    border: 1px solid black;
    *width: 100px;
}
```

