## 要求使用已知属性 [Require use of known properties](https://github.com/CSSLint/csslint/wiki/Require-use-of-known-properties)

可供CSS使用的属性变得越来越多，那么 在不检测属性名称是否正确时，我们就很容易将其拼写错误。

### 规则说明与示例

规则 ID: `known-properties`

此规则将检查每个使用的属性名称 以确保其是已知的属性。支持检查的属性 是CSS解析器中的一部分，规则使用CSS解析器的信息来验证 属性 是否为已知。支持检查的属性 将随CSS的开发完善而需要更新，虽然现在不是最终版，但毕竟是个避免错误的 好的开始。此规则就是在出现拼写错误时 提示警告。

所有游览器前缀属性 (以 - 开始) 将被忽略，因为前缀 会添加至 游览器各自版本的属性上，而这些属性没有一个参考标准。此规则将不同于传统的CSS验证，传统的CSS验证在 游览器前缀属性出现时 也会提示警告。

此规则不仅会检查 属性名称，也会检查属性 对应的值是否与其匹配。但现在，只能检查大部分而不是所有的属性对应的值 的合法性。

以下示例将提示警告:

```css
/* clr isn't a known property */
a {
    clr: red;
}

/* 'foo' isn't a valid color */
a {
    color: foo;
}
```

以下示例将 不提示警告:

```css
/* -moz- is a vendor prefix, so ignore */
a {
    -moz-foo: bar;
}
```

