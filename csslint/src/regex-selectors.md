## 不允许 选择器类似与表达式 [Disallow selectors that look like regular expressions](https://github.com/CSSLint/csslint/wiki/Disallow-selectors-that-look-like-regular-expressions)

CSS3增加了复杂的属性选择器 使得我们可以根据表达式来匹配 属性值。这系列的选择器有着性能的影响,表达式匹配与简单的类名匹配相比 速度要慢。在诸多场景里,是使用一个不确定值的选择器 还是 简单的给元素增加一个类名选择器 还在讨论中。这里有几种需要注意的属性选择器。

如属性选择器仅包含属性本身,则此属性选择器实际上没有性能问题。举个例子,以下选择器 仅匹配 `<a>`元素定义了`href`属性:

```css
//OK
a[href] {
    color: red;
}
```

此属性选择器能正常使用 并且 也不会造成任何性能问题。

如属性选择器使用确定的值作为匹配条件,则此属性选择器也是没问题的。举个例子,以下选择器 仅匹配`<a>`元素的`rel`属性值为 "external" :

```css
//OK
a[rel=external] {
    color: blue;
}
```

除以上两种情况,其它条件下使用属性选择器会造成性能问题。各属性选择器都有着类似的基本格式,在元素名称后使用方括号,与等号组合成的标识符,来进行表达式匹配。

### 包含

第一类"问题"选择器是  包涵选择器。选择器使用 `*=`来匹配 属性值中包涵给定的字符串 元素。工作原理类似与JavaScript中`indexOf()`方法,只要检索的值出现在属性值的任意位置即可,例子如下:

```css
a[href*=yahoo.com] {
    color: green;
}
```

此选择器匹配 任何`<a>`元素的`href`属性值中 有字符串 "yahoo.com"的条件。如下示例将匹配此条件:

```html
<a href="http://www.yahoo.com/">Yahoo!</a>

<a href="http://www.google.com/redirect=www.yahoo.com">Redirect to Yahoo!</a>

<a href="http://login.yahoo.com/">Login to Yahoo!</a>
```

注意 不必担心字符串两边是否有空格,因为只做部分匹配。

### 开始为

接着需要"避免使用"的选择器是 开始为匹配。选择器使用`^=`操作符来匹配 属性值以给定的字符串开头 元素。例子如下:

```css
a[rel^=ext] {
    color: red;
}
```

此规则将匹配如下示例:

```html
<a href="http://www.example.com" rel="external">Example</a>

<a rel="extra">Extra! Extra!</a>

<a rel="extreme">Extreme</a>
```

所有的选择器只关注 字符串"ext"是否在`rel`属性值的起始位置。

### 结尾为

接着需要"避免使用"的选择器是 结尾为匹配。选择器使用`$=`操作符来匹配 属性值以给定的字符串结尾 元素。例子如下:

```css
a[href$=.html] {
    color: blue;
}
```

此规则匹配所有 `<a>`元素 以 其`href`属性值为`.html`结尾的条件。以下示例将匹配:

```css
<a href="index.html">Home</a>

<a href="http://www.example.com/example.html">Example</a>
```

### 单词匹配

检查被空格间隔开的属性值,是更为复杂的选择器。选择器使用 `~=`操作符 来匹配 属性值必须包涵给定的单词,换句话说,属性值匹配给定单词的同时,属性值本身还须被空格所间隔开。示例如下:

```css
a[rel~=external] {
    color: red;
}
```

此规则将匹配如下例子:

```html
<a href="http://www.example.com" rel="external">Example</a>

<a href="http://www.example.com" rel="external me">Example</a>

<a href="http://www.example.com" rel="reference external">Example</a>

<a href="http://www.example.com" rel="friend external me">Example</a>
```

### 包涵破折号

最后一个"问题"选择器是 检查属性值中的字符串中是否被破折号分隔。`|=`用来找字符串的内部是否有`xxx-yyy-zzz`格式的字符串,例子如下:

```css
a[data-info|=name] {
    color: red;
}
```

它将匹配如下示例:

```html
<a data-info="name-address-phone">Info</a>

<a data-info="address-name-phone">Info</a>

<a data-info="address-phone-name">Info</a>
```

### 性能问题

以上所有这些复杂的属性选择器 都须通过一遍又一遍的计算来匹配对应属性值,从而确保最终的显示效果正确。为此,CSS需要开销更多的时间,来计算整个页面的显示效果。

### 规则详情

规则 ID:`regex-selectors`

此规则意在 标识出 存在影响性能问题的潜在选择器。为此,规则在发现选择器使用 `*=`,`|=`,`^=`,`$=`,`~=`提示警告。

以下示例 提示警告:

```css
.mybox[class~=xxx]{
    color: red;
}

.mybox[class^=xxx]{
    color: red;
}

.mybox[class|=xxx]{
    color: red;
}

.mybox[class$=xxx]{
    color: red;
}

.mybox[class*=xxx]{
    color: red;
}
```

以下示例 不会提示警告:

```css
.mybox[class=xxx]{
    color: red;
}

.mybox[class]{
    color: red;
}
```

