## 不允许重复属性 [Disallow duplicate properties](https://github.com/CSSLint/csslint/wiki/Disallow-duplicate-properties)

在早先网页开发中，相同的CSS属性出现了两次则毫无疑问是有问题的，特别是 如果有两个不同的值，如下:

```css
.mybox {
    width: 100px;
    width: 120px;
}
```

任何人看到此处的代码都清楚的知道是错误的。但是最近呢，复用属性可以用来解决 高低版游览器对CSS属性的支持度情况。举个例子，部分游览器支持RGBA色彩，而其它的则不行，那么出现以下的示例，就十分正常合理了:

```css
.mybox {
    background: #fff;
    background: rgba(255, 255, 255, 0.5);
}
```

此处重复很明显是有意为之。开发者想在支持RGBA的游览器上使用其效果，而不支持的游览器则使用传统的纯色。

### 规则说明与示例

规则 ID: `duplicate-properties`

此规则 意在找出重复定义的CSS属性代码。警告将出现在:

1. 属性出现两次且为相同的值。
2. 属性出现两次且被至少一个其它的属性所隔开。

以下示例将会提示警告:

```css
/* properties with the same value */
.mybox {
    border: 1px solid black;
    border: 1px solid black;
}

/* properties separated by another property */
.mybox {
    border: 1px solid black;
    color: green;
    border: 1px solid red;
}
```

以下示例将 不会提示警告:

```css
/* one after another with different values */
.mybox {
    border: 1px solid black;
    border: 1px solid red;
}
```

