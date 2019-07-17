## 不允许重复背景图片 [Disallow duplicate background images](https://github.com/CSSLint/csslint/wiki/Disallow-duplicate-background-images)

尽可能的使用较少的代码来完成功能，是高性能的准则之一。因此，同个URLS链接地址在CSS中只出现一次最好。如果你有多个样式类 需要使用同一背景图片，那么最好声明一个 包含此图片地址的通用样式类，接着 添加至需要使用的元素之上。请看下面代码:

```css
.heart-icon {
    background: url(sprite.png) -16px 0 no-repeat;
}

.task-icon {
    background: url(sprite.png) -32px 0 no-repeat;
}
```

在两个类中重复定义了背景图片地址。这是你本不需要的冗余代码，同时呢，当你修改了图片文件名，也增加了忘记同时修改文件中两处图片地址的可能性。一种解决方式为，抽取一个图片地址类(作为复用类)，然后将此类添加至原有HTML元素上。如下:

```css
.icons {
    background: url(sprite.png) no-repeat;
}

.heart-icon {
    background-position: -16px 0;
}

.task-icon {
    background-position: -32px 0;
}
```

这里,`icons`类指明了背景图片，其它类则指明背景图片的位置。

### 规则说明与示例

规则 ID: `duplicate-background-images`

此规则意在 确保同一链接地址不会在样式层叠表中重复。

以下示例将会提示警告:

```css
/* multiple instances of the same URL */
.heart-icon {
    background: url(sprite.png) -16px 0 no-repeat;
}

.task-icon {
    background: url(sprite.png) -32px 0 no-repeat;
}
```

以下示例将 不会提示警告:

```css
/* single instance of URL */
.icons {
    background: url(sprite.png) no-repeat;
}

.heart-icon {
    background-position: -16px 0;
}

.task-icon {
    background-position: -32px 0;
}
```

