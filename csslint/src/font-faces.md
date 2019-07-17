## 不使用过多网络字体 [Don't use too many web fonts](https://github.com/CSSLint/csslint/wiki/Don%27t-use-too-many-web-fonts)

网络字体越来越流行，`@font-face`使用频率也随之增加。但是，当字体文件过大，以及部分游览器在下载字体文件时,会阻塞渲染，就带来了显示性能的隐患。出于这个原因，CSSlint将在样式表中监测 出现超过 5次 网络字体引用时，提示警告。

