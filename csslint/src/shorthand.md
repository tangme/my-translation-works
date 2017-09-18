## 要求简写属性 [Require shorthand properties](https://github.com/CSSLint/csslint/wiki/Require-shorthand-properties)

有时咱们编写一条规则时,使用简写来代替多属性定义会更好,例如:

```css
.mybox {
    margin-left: 10px;
    margin-right: 10px;
    margin-top: 20px;
    margin-bottom: 30px;
}
```

此四属性可以组合成一个`margin`属性,如下:

```css
.mybox {
    margin: 20px 10px 30px;
}
```

使用简写属性可以帮助减少CSS体积的大小。

### 规则详情

规则 ID: `shorthand`

此规则意在 检索出可简写的属性来减少文件体积。因此,在如下示例中 提示警告:

1. 当`margin-left`,`margin-right`,`margin-top`,`margin-bottom`在同一规则中使用时。
2. 当`padding-left`,`padding-right`,`padding-top`,`padding-bottom`在同一规则中使用的。

以下示例 提示警告:

```css
.mybox {
    margin-left: 10px;
    margin-right: 10px;
    margin-top: 20px;
    margin-bottom: 30px;
}

.mybox {
    padding-left: 10px;
    padding-right: 10px;
    padding-top: 20px;
    padding-bottom: 30px;
}
```

以下示例 不提示警告:

```css
/* only two margin properties*/
.mybox {
    margin-left: 10px;
    margin-right: 10px;

}

/* only two padding properties */
.mybox {
    padding-right: 10px;
    padding-top: 20px;
}
```

