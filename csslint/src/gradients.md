## 要求定义所有渐变前缀 [Require all gradient definitions](https://github.com/CSSLint/csslint/wiki/Require-all-gradient-definitions)

截止2011年12月份，CSS渐变的标准定义还未定稿，也就是说 想跨游览器实现色彩渐变，需要使用很多不同的游览器前缀。到现在为止，CSS渐变 有五种 不同的游览器前缀。

- `-ms-linear-gradient` and `-ms-radial-gradient` for Internet Explorer 10+
- `-moz-linear-gradient` and `-moz-radial-gradient` for Firefox 3.6+
- `-o-linear-gradient` and `-o-radial-gradient` for Opera 11.10+
- `-webkit-linear-gradient` and `-webkit-radial-gradient` for Safari 5+ and Chrome
- `-webkit-gradient` for Safari 4+ and Chrome (aka "Old WebKit")

想跨游览器实现一个简单的双色渐变，须要代码如下:

```css
background: -moz-linear-gradient(top,  #1e5799 0%, #7db9e8 100%); /* FF3.6+ */
background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#1e5799), color-stop(100%,#7db9e8)); /* Chrome,Safari4+ */
background: -webkit-linear-gradient(top,  #1e5799 0%,#7db9e8 100%); /* Chrome10+,Safari5.1+ */
background: -o-linear-gradient(top,  #1e5799 0%,#7db9e8 100%); /* Opera 11.10+ */
background: -ms-linear-gradient(top,  #1e5799 0%,#7db9e8 100%); /* IE10+ */
```

在如此多的前缀里，编码中很容易忘记 少编写其中的一种或多个渐变前缀。

### 规则说明与示例

规则 ID: `gradients`

此规则在 使用渐变时 只定义部分游览器前缀 而未定义所有游览器前缀时，提示警告。

以下示例将提示警告:

```css
/* Missing -moz, -ms, and -o */
.mybox {
    background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#1e5799), color-stop(100%,#7db9e8));
    background: -webkit-linear-gradient(top,  #1e5799 0%,#7db9e8 100%);
}

/* Missing old and new -webkit */
.mybox {
    background: -moz-linear-gradient(top,  #1e5799 0%, #7db9e8 100%); 
    background: -o-linear-gradient(top,  #1e5799 0%,#7db9e8 100%);
    background: -ms-linear-gradient(top,  #1e5799 0%,#7db9e8 100%);
}
```

以下示例 不会提示警告:

```css
.mybox {
    background: -moz-linear-gradient(top,  #1e5799 0%, #7db9e8 100%);
    background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#1e5799), color-stop(100%,#7db9e8));
    background: -webkit-linear-gradient(top,  #1e5799 0%,#7db9e8 100%);
    background: -o-linear-gradient(top,  #1e5799 0%,#7db9e8 100%);
    background: -ms-linear-gradient(top,  #1e5799 0%,#7db9e8 100%); 
}
```

