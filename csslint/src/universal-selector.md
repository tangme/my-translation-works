## 不允许 通用选择器 [Disallow universal selector](https://github.com/CSSLint/csslint/wiki/Disallow-universal-selector)

通用选择器 (`*`) 匹配所有元素。尽管每次都能很方便的选择一组元素，但如果将其作为选择器的核心部分(选择器位置的最右侧) 则会造成性能问题。举个例子，如下的规则形式应该避免使用:

```css
.mybox * {
    background: #fff;
    color: #000;
    background: rgba(255， 255， 255， 0.5);
}
```

游览器按照从右至左的顺序解析选择器，因此这个规则将首先匹配文档中的所有元素。然后，逐一检测这些元素是否匹配下级规则，即是否拥有祖先样式`mybox`。如果包涵 `*` 的选择器越复杂，其解析的时间越久。正是因为此原因，推荐在使用 通用选择器时，避免将其放置选择器的最右侧。

### 规则详情

规则 ID: `universal-selector`

此规则意在 标示出 因为使用通用选择器而引起缓慢的样式规则。因此，在发现通用选择器 出现在 选择器的最右侧时 提示警告。

以下示例提示警告:

```css
* {
    color: red;
}

.selected * {
    color: red;
}
```

以下示例 不提示警告:

```css
/* universal selector is not key */
.selected * a {
    color: red;
}

```

