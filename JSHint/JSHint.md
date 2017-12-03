## JSHint Options (JSHint 配置选项)

[TOC]

### 必备选项

当设置为 true，以下选项将使JSHint在你的代码中提示更多的警告。

#### bitwise

此选项禁止使用诸如 ^ (XOR), \| (OR) 及其它的位操作符号。Bitwise(位操作符)在JavaScript编程中使用率极低，并且常常将 & 误敲击为 &&。

#### camelcase

注意 此选项不建议使用 并且将在下个JSHint主要发行版中移除。JSHint 限制了其本身是审查代码的正确性。如果你想检测代码书写规范，请访问 [the JSCS project. ](https://github.com/jscs-dev/node-jscs)

此选项 允许你强制所有变量名称使用 camelCase(驼峰法) 或者 UPPER_CASE(大写下划线组合)。

#### curly

此条件要求总是在 循环和条件语句后的代码块加上大括号。当代码块只有一条语句时JavaScript允许省略大括号，例子如下:

```javascript
while(day)
shuffle();
```

但是呢，某些情况下，这就会出现问题(试想sleep()是循环代码块的组成部份，但实际执行时却并不是)：

```javascript
while(day)
shuffle();
sleep();
```

#### enforceall

注意 此选项不建议使用 并且将在下个JSHint主要发行版中移除。如果用户不自主选择条目，其对应选项便不被维护。也就是说会导致超出预期的警告/错误，在更新JSHint小版本的时候。

此选项是在JSHint2.6.3版中提供快速配置JSHint的快捷方式。其能快速配置对应版本中：打开所有强制选项和关闭所有可选选项。

#### eqeqeq



