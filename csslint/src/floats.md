## 不允许过多的浮动 [Disallow too many floats](https://github.com/CSSLint/csslint/wiki/Disallow-too-many-floats)

`float`属性 是CSS中实现多列布局 广受欢迎的方式。在项目中，越来越多的`float`元素被用来创建不同的 页面布局或站点布局。如果此时改变布局，则会使得CSS代码十分脆弱，难以维护。

通常，使用很多的`float`意味 你的项目将得益于网格系统。CSS网格系统使用CSS类来实现标准的多列布局，一些热门的网格系统有:

- [960gs](http://960.gs/)
- [Blueprint](http://blueprintcss.org/)
- [OOCSS Grids](http://github.com/stubbornella/oocss/)
- [YUI Grids](http://yuilibrary.com/yui/docs/cssgrids/)
- [Twitter Bootstrap] ([http://getbootstrap.com](http://getbootstrap.com/))

使用以上其中一种网格系统，将极大的减少你需要编写的CSS代码。

### 规则说明与示例

规则 ID: `floats`

此规则 意在监察使用`float`次数从而减少代码复杂度。当`float`出现 超过10次时，将提示警告。使用float频率超过10次，意味着代码中有许多 多列布局的定义，那么通过引用网格系统框架，将更利于你的代码维护。