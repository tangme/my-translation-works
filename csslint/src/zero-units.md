## 不允许 零值有单位 [Disallow units for zero values](https://github.com/CSSLint/csslint/wiki/Disallow-units-for-zero-values)

在任何场景下,不论是长度单位还是百分比,使用 `0` 值而不指定单位,都是允许且正常运行的。在 `0px`,`0em`,`0%`,或其它 0值单位之间,均无任何差别。单位在这里并不重要,因为值本身 都会是 零。CSS允许咱们省略 零值的单位,并依旧视为合法的CSS。

推荐 移除所有长度为 零后面的单位;因为在游览器中规定的单位并不会起效,所以在安心移除的同时,还减小了文件体积。

### 规则详情

规则 ID: `zero-units`

此规则意在 标示出 长度为零 且带有单位的情形。因此,在发现 `0` 后跟随了单位或百分比时,提示警告。

以下示例 提示警告:

```css
.mybox {
    margin: 0px;
}

.mybox {
    width: 0%;
}

.mybox {
    padding: 10px 0px;
}
```

以下示例 不提示警告:

```css
.mybox {
    margin: 0;
}

.mybox {
    padding: 10px 0;
}
```

