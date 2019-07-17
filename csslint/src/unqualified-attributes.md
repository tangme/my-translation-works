## 不允许 未定义的属性选择器 [Disallow unqualified attribute selectors](https://github.com/CSSLint/csslint/wiki/Disallow-unqualified-attribute-selectors)

未定义属性选择器，如 `[type=text]`，首先匹配所有元素，然后检查各属性。这意味着 未定义选择器 和 通用选择器(`*`)一样都有着相同性能特点。和通用选择器相似，未定义属性选择器作为 选择器的核心部分(选择器最右侧)时，会造成性能问题。举个例子，如下规则定义 应当避免使用:

```css
.mybox [type=text] {
    background: #fff;
    color: #000;
    background: rgba(255， 255， 255， 0.5);
}
```

游览器以 从右至左的方式解析选择器，因而，此规则首先匹配文档中的所有元素，然后逐一检查对应属性。之后，再检查这些元素是否匹配下一级条件，即是否有祖先样式类 `mybox`。包涵未定义属性选择器的规则越复杂，判断的时间开销越久。正因如此，在使用 未定义属性选择器时，应避免将其放置最右侧。

### 规则说明与示例

规则 ID: `unqualified-attributes`

此规则意在 标示出 因使用未定义属性选择器而造成解析缓慢的规则。因此，在未定义属性选择器出现在规则最右侧时，提示警告。

以下示例提示警告:

```css
[type=text] {
    color: red;
}

.selected [type=text] {
    color: red;
}
```

以下示例 不提示警告:

```css
/* unqualified attribute selector is not key */
.selected [type=text] a {
    color: red;
}
```

