## JSHint Options (JSHint 配置选项)

[TOC]

### 必备选项

当设置为 true，以下选项将使JSHint在你的代码中提示更多的警告。

#### bitwise

此选项禁止使用诸如 `^` (XOR), `|` (OR) 及其它的位操作符号。Bitwise(位操作符)在JavaScript编程中使用率极低，并且常常将 `&` 误敲击为 `&&`。

#### camelcase

**注意** 此选项不建议使用 并且将在下个JSHint主要发行版中移除。JSHint 限制了其本身是审查代码的正确性。如果你想检测代码书写规范，请访问 [the JSCS project. ](https://github.com/jscs-dev/node-jscs)

此选项 允许你强制所有变量名称使用 camelCase(驼峰法) 或者 UPPER_CASE(大写下划线组合)。

#### curly

此条件要求总是在 循环和条件语句后的代码块加上大括号。当代码块只有一条语句时JavaScript允许省略大括号，例子如下:

```javascript
while(day)
shuffle();
```

但是呢，某些情况下，这就会出现问题(试想`sleep()`是循环代码块的组成部份，但实际执行时却并不是)：

```javascript
while(day)
shuffle();
sleep();
```

#### enforceall

**注意** 此选项不建议使用 并且将在下个JSHint主要发行版中移除。如果用户不自主选择条目，其对应选项便不被维护。也就是说会导致超出预期的警告/错误，在更新JSHint小版本的时候。

此选项是在JSHint2.6.3版中提供快速配置JSHint的快捷方式。其能快速配置对应版本中：打开所有强制选项和关闭所有可选选项。

#### eqeqeq

此选项不准许使用 `==` 和 `!=` 允许并推荐使用 `===` 和 `!==` 。前者会在比较之前，进行值的强制转换，从而导致某些预计不到的问题。后者则不会做任何的强制转换，因此通常来看会更合理安全一些。如果你想了解更多关于JavaScript值的强制转换信息，我们推荐您阅读Angus Croll的文章 [Truth, Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/) 。

#### es3

**注意**  此选项已不推荐使用并将在JSHint主要版本中移除。请使用 `esversion: 3` 代替。

此选项告知JSHint 你的代码须遵循 ECMAScript 3规范。如果你的程序需要在早期游览器运行－－例如 IE 6/7/8/9 及早期JavaScript环境的话，请使用此选项。

#### es5 

**注意**  此选项已不推荐使用并将在JSHint主要版本中移除。请使用 `esversion: 5` 代替。

此选项允许定义  [the ECMAScript 5.1 specification](http://es5.github.io/) 规范中的语法。

这包括允许使用 保留关键字 作为对象的属性。

#### esversion

此选项用于指出代码须遵循的 ECMAScript 版本。其值可以为以下任意一种:

* 3 － 如果你的程序需要在早期游览器运行－例如 IE 6/7/8/9 及早期JavaScript环境的话，请使用此选项
* 5 － 此选项允许定义  [the ECMAScript 5.1 specification](http://es5.github.io/) 规范中的语法。这包括允许使用 保留关键字 作为对象的属性
* 6 － 告知 JSHint 你的代码使用 [ECMAScript 6](http://www.ecma-international.org/ecma-262/6.0/index.html) 规范。注意 并非所有游览器支持实现其规则。

#### forin

此选项要求所有 `for in` 循环过滤 对象属性。for in 句式允许迭代循环出对象的所有名称，包括那些继承至原型链的。此行为会导致在你的对象中出现预想不到的属性，因此，为了确保安全，通常过滤掉继承的属性，参考如下例子：

```javascript
for (key in obj) {
  if (obj.hasOwnProperty(key)) {
    // 这里确定 obj[key] 属于对象本身 并且 不是来自于继承
  }
}
```

更深入的理解 JavaScript 中的 `for in` 循环，请阅读 Angus Croll 文章 [Exploring JavaScript for-in loops](http://javascriptweblog.wordpress.com/2011/01/04/exploring-javascript-for-in-loops/) 

#### freeze

此选项不允许重写内置对象的原型，例如 `Array`,`Date` 等等

```javascript
// jshint freeze:true
Array.prototype.count = function (value) { return 4; };
// -> 警告: 扩展了内置对象的原型:'Array'
```

#### funcscope

此选项 在把变量声明在控制语句内部，随后在外部使用时 不提示警告。尽管 JavaScript 只有两种真正的作用域 － 全局作用域 和 函数(方法)作用域 － 但这样使得刚接触这门语言的人难以理解与调试问题。这也是在默认情况下，JSHint 发现 变量使用在其预计作用域之外 提示警告。

```javascript
function test() {
  if (true) {
    var x = 0;
  }

  x += 1; // 默认情况: 'x' 在作用域之外使用.
            // 当 funcscope:true 时，将不会提示警告
}
```

#### futurehostile

此选项在发现使用 JavaScript 后期新版保留标识符时 提示警告。尽管重写这些并未实现的保留标识符 不会有任何影响，但其可能导致后期将 代码库升级至新版时 发生问题。

#### globals

