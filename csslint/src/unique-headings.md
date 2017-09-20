## 标题应只定义一次 [Headings should only be defined once](https://github.com/CSSLint/csslint/wiki/Headings-should-only-be-defined-once)

面相对象CSS (OOCSS) 要求定义可重用的对象,以确保在站点的任何位置使用时,都有着相同的显示效果。标题元素 (h1 - h6) 应当作为内建对象考虑,使其不管在何处使用均为同样的显示效果。因此,每个标题元素,因当只被规则定义一次。多处规则定义相同的标题显示效果,会使其很难使用,因为 标题样式会因为上下文环境不一致而出现不同展示效果。

### 规则详情

规则 ID:`unique-headings`

此规则意在 标识出重复定义标题元素的声明。因此,警告出现在 对同一标题 定义了多个规则时。

以下示例提示警告:

```css
/* Two rules for h3 */
h3 {
    font-weight: normal;
}

.box h3 {
    font-weight: bold;
}
```

以下示例 不提示警告:

```css
/* :hover doesn't count */
h3 {
    font-weight: normal;
}

h3:hover {
    font-weight: bold;
}
```

