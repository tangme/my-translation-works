## 不允许 下划线前缀 [Disallow underscore hack](https://github.com/CSSLint/csslint/wiki/Disallow-underscore-hack)

下划线前缀 是仅对IE7以前版本的游览器执行CSS属性的一种技术手段。通过在属性名前添加下划线，老版IE游览器将省略下划线，而其它游览器则直接忽略此属性。示例如下:

```css
.mybox {
    border: 1px solid black;
    padding: 5px;
    width: 100px;
    _width: 200px;
}
```

在这个例子中，IE6及以前游览器把`_width`属性 当`width`看待，所以实际宽度为`200px`;其它游览器则跳过此属性，因而实际值为`100px`。

下划线前缀是依赖IE游览器，CSS解析的缺陷 实现其效果，正因如此，非特殊情况并不推荐使用。

### 规则说明与示例

规则 ID: `underscore-property-hack`

此规则意在 消除在CSS中使用下划线前缀。因此，在属性名前出现下划线 将提示警告:

```css
.mybox {
    border: 1px solid black;
    _width: 100px;
}
```

