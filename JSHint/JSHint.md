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

**注意** 此选项不建议使用并且将在下个 JSHint 主要发行版中移除。JSHint 限制了其本身是用来检测代码的正确性。如果你想提高编码的风格可阅读性，请参看 [the JSCS project](https://github.com/jscs-dev/node-jscs).

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

#### newcap

**注意** 此选项不建议使用并且将在下个 JSHint 主要发行版中移除。JSHint 限制了其本身是用来检测代码的正确性。如果你想提高编码的风格可阅读性，请参看 [the JSCS project](https://github.com/jscs-dev/node-jscs).

此选项 要求大写构造函数的名称。大写函数名称意在 函数与 `new` 操作符使用时，可以直观的帮助程序区分此函数是构造函数还是其它类型的函数，以便避免使用 `this` 点属性时的错误。

当然不按此大写风格编码，并不会影响代码在各游览器或环境中运行，但是在阅读代码时则很难推敲出是否可用 new 操作。也正是这点的重要性，因为当函数意在使用 `new` 操作符时却没有使用，那么 `this` 将指向全局的对象 而不是 new 出来的对象。

#### noarg

此选项不允许使用 `arguments.caller` 和 `arguments.callee`. `.caller` 和 `.callee`使得没有优化的可能性，因此在之后的JavaScript版本中不建议使用。并且实际上，ECMAScript 5 在严格模式下 已禁止使用 `arguments.callee`.

#### nocomma

此选项禁止使用 逗号操作符。当其被误用(滥用)时，逗号操作符会模糊语句所表达的值或者造成错误的代码。

#### noempty

**注意** 此选项不建议使用并且将在下个 JSHint 主要发行版中移除。JSHint 限制了其本身是用来检测代码的正确性。如果你想提高编码的风格可阅读性，请参看 [the JSCS project](https://github.com/jscs-dev/node-jscs).

此选项 当检测出代码中出现空代码块时 提示警告。JSLint 本身在检测所有空代码块时即提示警告，这里仅简单的提供一个设置选项。最后需要指出的是 并没有任何研究报告指出 空代码块在 JavaScript 中会对代码造成任何影响。

#### nonbsp

此选项警告在 "非中断空格" 字符串。此字符串在Mac电脑中敲击 option-space时出现，在非UTF-8的网页上 会有潜在的中断可能。

#### nonew

此选项禁止使用 构造函数以避免其副作用。一些编程人员在调用构造函数时并未将其返回值分配给任何变量:

```javascript
new MyConstructor();	
```

在这段代码中 对象通过 `new` 操作符调用 `MyConstructor` 创建后，并未在任何地方使用，看不出其使用目的；因而在编码中要避免如上的情形。

#### notypeof

此选项当发现 `typeof` 操作符的值不正确时，不提示警告。此操作符只会  [限定可能的返回值](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)。默认情况下，JSHint 警告于 我们由于输入错误而造成的比较值

```javascript
//  应该输入 'function' 而不是 'fuction'
if (typeof a == "fuction") { // 输入了错误的值 'fuction'
  // ...
}
```

请不要使用此选项，除非你肯定的知道你不想使用此检测。

#### predef

此选项允许你配置变量告知 JSHInt 这些变量隐式声明在环境中。配置项通过定义字符串数组完成。变量名的前缀中含有 (-) 字符时，将会从预先定义的变量集合中移除。

JSHint 会认为以此方式声明的变量仅为可读。

此选项不能在内嵌配置中指定；其只能经 JavaScript API 或 外部配置文件实现。

#### quotmark

**注意** 此选项不建议使用并且将在下个 JSHint 主要发行版中移除。JSHint 限制了其本身是用来检测代码的正确性。如果你想提高编码的风格可阅读性，请参看 [the JSCS project](https://github.com/jscs-dev/node-jscs).

此选项在代码中保证 引号 使用的一致性。有三种值的设置： `true` 可混用单引号 双引号 但须保证其配对的一致，`single` 仅允许使用 单引号，`double` 仅允许使用双引号。

#### shadow

此选项 检测变量重复定义时 是否提示警告，换句话说 如果定义了一个变量且此变量已在外部某处定义过，提示是否警告。

* "inner" 仅检测相同的作用域
* "outer" 检测相同 和 外部作用域
* "false" 与 inner配置一致
* "true" 允许变量重复定义

#### singleGroups

此选项 在非严格要求下禁止使用组操作符。如下为一个 错误使用的一元运算符。

```javascript
// jshint singleGroups: true

delete(obj.attr); // Warning: 无用的组操作符
```

#### strict

此选项要求 编码能在ECMAScript 5 严格模式下运行。 [严格模式](https://developer.mozilla.org/en/JavaScript/Strict_mode) 给多变的 JavaScript 用法作了一定限制。严格模式消除了一些 JavaScript 潜在的编码理解错误或缺陷，通过改变其所产生的错误并不会造成错误。同时也修复了以此给 JavaScript 引擎实现最佳效能问题的错误。

* "global" - 在全局层面必须有 `"use strict"` 指令

* "implied"

* false - 不启用严格模式

* true - 在函数层面必须有 `"use strict"` 指令

  * ```
    相比于全局启用严格模式 此方式更适合于脚本的加载，因为全局启用反而会影响页面加载其它的脚本
    ```

#### undef

此选项禁止使用未定义过的变量名。此设置对于 遗漏和键入错误 非常有帮助。

```javascript
// jshint undef:true

function test() {
  var myVar = 'Hello, World';
  console.log(myvar); // 啊，键入错误. JSHint 将提示未定义警告
}

```

如果变量定义在其它文件里，可以使用 `global` 选项来配置。

#### unused

此选项 在检测出定义过的变量却从未使用过时 提示警告。这对于保证代码清晰特别有益，可以说是 `undef` 的变相版。

```javascript
// jshint unused:true

function test(a, b) {
  var c, d = 2;

  return a + d;
}

test(1, 2);

// Line 3: 'b' 虽定义 但从未使用
// Line 4: 'c' 虽定义 但从未使用
```

对了，此选项在检测到 配置在 `global`指令中的全局变量，未使用时， 提示警告。

此选项也可以设置 `vars` 用以只检测变量，而忽略函数的参数，或者设置 `strict` 检测 所有变量与函数参数。默认参数 (true) 时，允许未使用的参数 随使用过的参数一起。

#### varstmt

当设置为 true 时，禁止使用 var 。如下：

```javascript
// jshint varstmt: true

var a; // Warning: `var` 声明禁止. 请使用 `let` or `const` 代替.
```

### 可选选项

当设置为 true,以下选项将使 JSHint 提示较少警告。

#### asi

此选项设置 在缺失分号下 不提示警告。在各社区论坛里，很多人都散布着有关对分号的疑惑不确定。一个普通的共识就是 分号 需要在所有的语句后结束。JavaScript关于分号所制定的规则被所有游览器所遵循，因此是否需要在代码中使用分号 由你决定。

更多关于 JavaScript 的分号信息可阅读 Isaac Schlueter 的  [An Open Letter to JavaScript Leaders Regarding Semicolons](http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding) 和  [JavaScript Semicolon Insertion](http://inimino.org/~inimino/blog/javascript_semicolons).

#### boss

此选项 在比较表达式错用为赋值时 不提示警告。通常情况下，编码如 `if (a = 10) {}` 被看作拼写错误。但是，在如下情况是有效的：

```javascript
for (var i = 0, person; person = people[i]; i++) {}
```

可以在两侧加上圆括号包围赋值语句以取消情况，如下：

```javascript
for (var i = 0, person; (person = people[i]); i++) {}
```

#### debug

此选项 在代码中出现 `debugger` 语句时，不提示警告。

#### elision

此选项告知 JSHint 你的代码使用 ES3 数组省略元素，或孔元素 例如 `[1,,,4,,,7]` .

#### eqnull

此选项 检测出 `==null` 比较时，不提示警告。此比较用法在你想检测变量是 `null` 或  `undefined` 时十分有效。

#### esnext

**注意** 此选项不建议使用，并将在下个 JSHint 的主要版本中移除。请用 `esversion: 6` 代替。

此选项告知 JSHint 你的代码使用 ECMAScript 6 语法规则。注意 并非所有游览器都实现了此版本中的特性。

更多信息请看 

- [Specification for ECMAScript 6](http://www.ecma-international.org/ecma-262/6.0/index.html)

#### evil

此选项 发现使用 `eval` 时，不提示警告。 不推荐使用 `eval`，因为在各种脚本注入攻击下会使得代码十分脆弱，并且 JavaScript 引擎也难以达到最高效运行。

#### expr

此选项 在应当使用赋值 或 函数调用 却使用表达式时，不提示警告。大多数情况下出现此现象是因为键入错误。但是，特殊情形下也有此需求，这也就是此配置项需要注意的地方。

#### globalstrict

**注意** 此选项不建议使用并且将在下个JSHint的主要发行版中移除。请使用 `strict: "global"`.

此选项在使用 全局严格模式下 不提示警告。全局严格模式会对第三方插件造成影响，因此不推荐使用。

更多关于严格模式的信息可见 `strict` 选项。	

#### lastsemic

此选项 在发现缺失分号时 不提示警告，但只适用于单行代码块:

```javascript
var name = (function() { return 'Anton' }());
```

这在当你使用 JavaScript 代码自动生成器时，变得很实用。

#### laxbreak

**注意** 此选项不建议使用 并且将在下个JSHint主要发行版中移除。JSHint 限制了其本身是审查代码的正确性。如果你想检测代码书写规范，请访问 [the JSCS project. ](https://github.com/jscs-dev/node-jscs)

此选项在 关闭绝大多数 代码中不安全换行的警告。在逗号首行编码格式中依旧提示警告。如想关闭此警告，可以参看 `laxcomma` (见下方)。

#### laxcomma

**注意** 此选项不建议使用 并且将在下个JSHint主要发行版中移除。JSHint 限制了其本身是审查代码的正确性。如果你想检测代码书写规范，请访问 [the JSCS project. ](https://github.com/jscs-dev/node-jscs)

此选项将关闭 首行逗号编码格式警告：

```javascript
var obj = {
    name: 'Anton'
  , handle: 'valueof'
  , role: 'SW Engineer'
};
```

#### loopfunc

此选项关闭 循环体内定义函数的警告。在循环体内部定义函数会导致如下错误：

```javascript
var nums = [];

for (var i = 0; i < 10; i++) {
  nums[i] = function (j) {
    return i + j;
  };
}

nums[0](2); // 输出 12 而不是 2
```

修复如上代码，你需要复制一份 i 的值：

```javascript
var nums = [];

for (var i = 0; i < 10; i++) {
  (function (i) {
    nums[i] = function (j) {
        return i + j;
    };
  }(i));
}
```

