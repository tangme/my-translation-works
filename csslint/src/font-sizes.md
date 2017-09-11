## 不使用过多的字体大小声明 [Don't use too many font size declarations](https://github.com/CSSLint/csslint/wiki/Don%27t-use-too-many-font-size-declarations)

一个利于维护的站点,通常都有通用的字体集。这些字体大小,往往定义在一个代表其含义的抽象类当中,以便运用到站点的各个使用场景。如果未抽取出公用类。会导致开发者频繁的使用`font-size`,来使元素大小按预期显示。这就带来了一个问题,当设计的字体大小改变后,我们需要改变样式中所有设计的字体大小。而抽取出类时,只用改变类中定义的大小即可做到全局调整。

你可以创建一些标准字体大小类,如:

```css
.small {
    font-size: 8px;
}

.medium {
    font-size: 11px;
}

.large {
    font-size: 14px;
}
```

在你的项目中使用以上类,能确保字体大小的一致性 贯穿始终,也限制了`font-size`在CSS文件中出现的次数。此时,只需要改变一处字体大小的设置，就可实现之前需要修改多处的效果。

### 规则详情

规则 ID:`font-sizes`

此规则意在强调 将过多的使用字体大小,转而至 统一定义为一个类的好处。规则 在使用 `font-size` 超过10次时 提示警告。