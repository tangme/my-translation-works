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

此选项用于定义一组 未在源代码中声明全局变量的白名单。其在与 `undef` 选项结合使用，用以取消警告 项目全局变量时，十分有用。

设置为 `true` 允许对变量 读 写 操作。

设置为 `false` 将提示JSHint 把变量作为只读。

也可参看 "environment" 选项：一个选项组 用以快速定义JavaScript环境中的全局变量。

把 `globals` 配置为一个单一文件，请参看  [Inline Configuration](http://jshint.com/docs/#inline-configuration).

#### immed

**注意** 此选项不建议使用并且将在下个 JSHint 主要发行版中移除。JSHint 限制了其本身是用来检测代码的正确性。如果你想提高编码的风格可阅读性，请参看 [the JSCS project](https://github.com/jscs-dev/node-jscs).

此选项禁止使用 未用圆括号包围的即时函数。圆括号包围的表达式有助于读者理解你的代码是表达 函数的结果，而不是函数本身。

#### indent

**注意** 此选项不建议使用并且将在下个 JSHint 主要发行版中移除。JSHint 限制了其本身是用来检测代码的正确性。如果你想提高编码的风格可阅读性，请参看 [the JSCS project](https://github.com/jscs-dev/node-jscs).

此选项 提示在代码中设置一个 tab 宽度，便于阅读。

#### iterator

此选项 在检测到使用 `__iterator__` 属性时，不提示警告。此属性并未被所有游览器支持，请谨慎使用。

#### latedef

此选项禁止 定义变量之前使用变量。JavaScript 仅有函数作用域，除此之外，所有的变量都会移动置顶到全局作用域。此默认行为会导致某些非常糟糕的问题，因此为了更安全的使用变量，请在变量定义之后再调用。

将选项值设置为 "nofunc" 将允许忽略 函数声明。

更多深入的了解 JavaScript 作用域及作用域提升，可阅读 Ben Cherry 的 [JavaScript Scoping and Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting) 。

#### maxcomplexity

此选项 使你得以控制代码的圈复杂度。圈复杂度测量计算程序源码中独立语句个数。更多信息请参看  [cyclomatic complexity on Wikipedia](http://en.wikipedia.org/wiki/Cyclomatic_complexity).

#### maxdepth

此选项 提供你设置代码块嵌套的层级数量:

```javascript
// jshint maxdepth:2

function main(meaning) {
  var day = true;

  if (meaning === 42) {
    while (day) {
      shuffle();

      if (tired) { // JSHint: 代码块嵌套过深 (3层嵌套).
          sleep();
      }
    }
  }
}
```

#### maxerr

此选项 供你设置最大的警告数量，如警告超过最大数 JSHint 将不再检测其后合法性。默认值: 50 .

#### maxlen

注意** 此选项不建议使用并且将在下个 JSHint 主要发行版中移除。JSHint 限制了其本身是用来检测代码的正确性。如果你想提高编码的风格可阅读性，请参看 [the JSCS project](https://github.com/jscs-dev/node-jscs).

此选项 提供设置每行代码的最大长度。

#### maxparams

此选项 提供设置每个 函数(方法) 的最大形参个数:

```javascript
// jshint maxparams:3

function login(request, onSuccess) {
  // ...
}

// JSHint: 形参个数过度 (4个参数).
function logout(request, isManual, whereAmI, onSuccess) {
  // ...
}
```

#### maxstatements

此选项 提供设置 每个函数(方法)体内 的最大语句条数:

```javascript
// jshint maxstatements:4

function main() {
  var i = 0;
  var j = 0;

  // 函数(方法)声明只当作一条雨具.
  // 其内部语句条数不会计算至 所属外部的函数(方法)中.
  function inner() {
    var i2 = 1;
    var j2 = 1;

    return i2 + j2;
  }

  j = i + j;
  return j; // JSHint: 语句过多 (5条语句)
}
```

