## 不允许 过度定义选择器 [Disallow overqualified elements](https://github.com/CSSLint/csslint/wiki/Disallow-overqualified-elements)

编写如`li.active`选择器是不必要的，除非 不同的元素名称，在使用相同类名下 需要展示不同的样式。多数情况下，在选择器中移除元素名称更为妥当，不仅减小了CSS文件的体积，同时也提升了选择器的性能(不须再次匹配元素)。

移除元素名称也同时降低了CSS与HTML的耦合度，允许你改变元素使用的样式类，而不需要更新CSS样式文件。

### 规则说明与示例

规则 ID: `overqualified-elements`

此规则意在 移除冗余不必的选择器总而减少数据大小。为此，警告出现在 元素名称与类名同时使用时(如 `li.active`)。如果，两个不同的元素使用了相同的类名(如 `li.active`  `p.active`) 将 不会提示警告。

以下示例 提示警告:

```css
div.mybox {
    color: red;   
}

.mybox li.active {
    background: red;
}
```

以下示例将 不提示警告:

```css
/* Two different elements in different rules with the same class */
li.active {
    color: red;
}

p.active {
    color: green;
}
```

