## 预防字体引用错误 [Bulletproof font face](https://github.com/CSSLint/csslint/wiki/Bulletproof-font-face)

当使用`@font-face`来 跨游览器声明 多字体类型时,你会发现在老版IE中出现404错误,这是因为老版IE在解析字体声明时的缺陷。来,举个例子,看如下语法:

```css
@font-face {
    font-family: 'MyFontFamily';
    src: url('myfont-webfont.eot') format('embedded-opentype'), 
        url('myfont-webfont.woff') format('woff'), 
        url('myfont-webfont.ttf')  format('truetype'),
        url('myfont-webfont.svg#svgFontName') format('svg');
}
```

在IE6,7和8上将为出现404错误。解决方式 是在第一个字体链接后加上 ? (问号),接下来 IE 会把 余下的属性值看作查询字符串。以下为正确示例:

```css
@font-face {
    font-family: 'MyFontFamily';
    src: url('myfont-webfont.eot?#iefix') format('embedded-opentype'), 
        url('myfont-webfont.woff') format('woff'), 
        url('myfont-webfont.ttf')  format('truetype'),
        url('myfont-webfont.svg#svgFontName') format('svg');
}
```

### 规则详情

规则 ID: `bulletproof-font-face`

此规则意在防止 在IE8及早期游览器上 因为解析字体链接的缺陷而产生的404错误。

以下示例会出现警告:

```
@font-face {
    font-family: 'MyFontFamily';

    /* First web font is missing query string */
    src: url('myfont-webfont.eot') format('embedded-opentype'), 
        url('myfont-webfont.woff') format('woff'), 
        url('myfont-webfont.ttf')  format('truetype'),
        url('myfont-webfont.svg#svgFontName') format('svg');
}
```

以下示例将 不会 出现警告:

```
@font-face {
    font-family: 'MyFontFamily';
    src: url('myfont-webfont.eot?#iefix') format('embedded-opentype'), 
        url('myfont-webfont.woff') format('woff'), 
        url('myfont-webfont.ttf')  format('truetype'),
        url('myfont-webfont.svg#svgFontName') format('svg');
}
```

此规则要求 第一个字体声明为 带查询字符串的 .eot文件,但不会检测余下的字体链接(这不是重点,假定你已有了.eot文件)