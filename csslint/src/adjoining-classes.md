## 不使用相邻类 [Disallow adjoining classes](https://github.com/CSSLint/csslint/wiki/Disallow-adjoining-classes)

相邻类,也可以称之为类链,像`.foo.bar` .在CSS规范中允许使用,但在IE6即更早版本中可能就不好使了.IE仅仅会以'.bar'的形式匹配选择器,也就是说你的选择器不会按你的套路出牌,顺便出现了跨游览器bugs.(不用IE6的 放心大胆的使用吧)

通常来说,基于单类来定义一个样式要比多类定义更好.可以瞅瞅想想下面的例子:

```css
.foo {
    font-weight: bold;
}
.bar {
    padding: 10px;
}
.foo.bar {
    color: red;
}
```

选择器`.foo.bar`的规则,可以用一个新类进行重写:

```css
.foo {
    font-weight: bold;
}
.bar {
    padding: 10px;
}
.baz {
    color: red;
}
```

那么这个新类,`baz`,必须添加至原有的HTML元素上.这实际上更利于维护,因为`.baz`此规则此刻就可以被复用了，而`.foo.bar`规则只能被用在前一种固有的情况下.

### 规则详情

规则 ID: `adjoining-classes`

此规则意在指出 使用相邻类时,在IE6即更早版本时会出现匹配失败的情况。

以下例子将会出现警告:

```css
.foo.bar {
    border: 1px solid black;
}
.first .abc.def {
    color: red;
}
```

以下例子将不会出现警告:

```css
/* 两个类中间有空格 */
.foo .bar {
    border: 1px solid black;
}
```

