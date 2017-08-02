#### javascript编码标准
javascript已经成为开发基于wordpress基础应用以及wordpress核心的重要组件。对于格式化和样式化JavaScript代码，以保持与WordPress标准提供的核心PHP、HTML和CSS代码相同的代码一致性，需要使用标准。
> 在任何代码库中的代码都应该看起来像一人所为，不论有多少人参与开发-[ Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js/) (编写一致性，惯用的javascript的原则)

wordpress javascript编码标准是根据[ jQuery JavaScript Style Guide](https://contribute.jquery.org/style-guide/js/)改编而成。我们的标准不同于jquery的手册的地方有以下几点:
- wordpress在字符串声明的时候使用单引号标记
- case声明被放在了switch区域内
- 函数内容总是缩进的，包含了全文件闭包封装器。
- 为了wordpress php编码标准的一致性，某些whitespace的规则不同。
- jquery的100字符的强硬限制是受鼓励的，但是并没有严格执行。
下面的许多实例都直接从JQUERY的样式指南中改编；这些不同已经被整合在了这个页面中的实例里。对于wordpress代码来说下面任何标准和实例都该被认为是最佳实践，除非明确的说它是个反面例子。

#### 代码重构
> “[Code refactoring should not be done just because we can](https://make.wordpress.org/core/2011/03/23/code-refactoring/)”(代码重构不应该是仅因为我们能够做到) -开发主管 Andrew Nacin

wordpress代码结构中的javascript的许多部分不符合它们的风格。wordpress在这方面进行了优雅升级，这样代码就会变得简洁，干净，一目了然。

尽管推出标准是重要的，仅仅为了符合标准重写老旧的JS文件不是一个紧急的问题。针对老文件作出“whitespace-only”这样的补丁是强烈不推荐的。

所有新的JS代码或者更新都要被重审以确保它符合标准，并且能通过JSHint。

#### 空格
在你的代码中大方的使用空格，“当有疑问的时候，分隔开”.

为了提升开发的可读性，这些规则鼓励使用空格。压缩过程创建了一个文件，以优化浏览器的阅读和处理。
- 用tabs缩进
- 在行的末尾或者在新的行没有空白行。
- 一行通常不超过80个字符，不能超过100个(tab算4个空格)。这是一个软规则，但是长的行通常就意味着可读性差和代码的紊乱。
- ``` if```/```else```/```for```/```while```/```try``` 这些地方都应该一直使用大括号，而且总是多行。
- 像（++，--等等）这种一元操作符，中间不能有空格。
- 任何```,```和```:```不能有前置空格。
- 任何```;``` 作为一个声明的界定符的时候都应该在行的末尾。
- 任何在定义对象时的属性名之后的```:```，不能有前置空格。
- 在三元控制符中的```?```和```：```都应该两边有空格。
- 在空的(```{}```,```[]```,```fn()```等等)结构中不能有空格。
- 在每个引用文件后应该另起一行。
- 任何```!```否定操作都应该有以下空格。
- 所有函数体都用一个tab来缩进，甚至是那些全部被封装在闭包内的文件。
- 空格也许可以使文档或者行中的代码对齐，但是只有tab才能用于行的开头。
wordpress的javascript标准比jquery style指南更喜欢使用宽松的空白行规则一点。这些差异是为了在wordpress的代码库中php和javascript文件的一致性。

空白行可以很容易的在一行的末尾累积-为了避免这个，一个尾部的空白行在JSHint中会被当做一个error来抓取，增强抓取空白行的方式是在你的文本编辑器下启用可见空白行字符（visible whitespace characters ）。

#### 对象
对象声明可以是一个单独的行如果它们很短的话(记住指南中的行长度)，当对象声明是一行且太长，就必须一行一个属性。如果是关键字或包含特殊字符的属性名就需要引号:
```
// 最好的方式
var map = {
    ready: 9,
    when: 4,
    'you are': 15
};

// 对于小的对象是可以接受的
var map = { ready: 9, when: 4, 'you are': 15 };

// 最差的方式
var map = { ready: 9,
    when: 4, 'you are': 15 };

```
#### 数组和函数的调用
总是用额外的空格来包住元素和参数:
```
array = [ a, b ];

foo( arg );

foo( 'string', object );

foo( options, object[ property ] );

foo( node, 'property', 2 );

```
例外:
```
// 为了我们PHP标准的一致性, 不要包含一个空格
// 在数组表示法中字符串文本或者整数被用作键值:
prop = object['default'];
firstArrayElement = arr[0];

// 只有回调，对象或者数组作为唯一参数的函数
// 参数的两边都没有空格
foo(function() {
    //要执行的代码
});

foo({
    a: 'alpha',
    b: 'beta'
});

foo([
    'alpha',
    'beta'
]);

// 具有回调，对象，或者数组作为第一个参数的函数:
// 第一个参数之前没空格
foo(function() {
    //要执行的代码
}, options );

// 具有回调，对象，或者数组作为最后一个参数的函数:
// 在最后一个参数之后没有空格
foo( data, function() {
    //要执行的代码
});

```

#### 空格用的好的例子
```
var i;

if ( condition ) {
    doSomething( 'with a string' );
} else if ( otherCondition ) {
    otherThing({
        key: value,
        otherKey: otherValue
    });
} else {
    somethingElse( true );
}

// 不像jquery，wordpress更喜欢在```!```否定操作符后使用一个空格.
// 这也是为了符合我们的php标准.
while ( ! condition ) {
    iterating++;
}

for ( i = 0; i < 100; i++ ) {
    object[ array[ i ] ] = someFn( i );
    $( '.container' ).val( array[ i ] );
}

try {
    // Expressions
} catch ( e ) {
    // Expressions
}

```

#### 分号
使用它们，不要依赖于自动插入分号(ASI)。
#### 缩进和换行符
缩进与换行给复杂语句增加可读性。

tab用于缩进，当全部文件被包含在一个闭包中(一个立即执行函数)，函数的内容应该用一个tab缩进:
```
(function( $ ) {
    // Expressions indented

    function doSomething() {
        // Expressions indented
    }
})( jQuery );

```

#### 块和大括号
``` if```/```else```/```for```/```while```/```try``` 块应该总是使用大括号，并且总是用多行，在函数定义的时候开始大括号应该与其在同一行，条件判断或者循环的时候也是。闭合大括号应该在如下的块的最后的新的一行
```
var a, b, c;

if ( myFunction() ) {
    // Expressions
} else if ( ( a && b ) || c ) {
    // Expressions
} else {
    // Expressions
}

```

#### 多行语句
当一行的一个语句太长的时候，就必须要在一个操作符后面换行。
```
// 不好的
var html = '<p>The sum of ' + a + ' and ' + b + ' plus ' + c
    + ' is ' + ( a + b + c );

// 好的
var html = '<p>The sum of ' + a + ' and ' + b + ' plus ' + c +
    ' is ' + ( a + b + c );

```
行应该分成逻辑组如果其提升了可读性的话，例如将一个三元操作符拆分其表达式到各自的行，虽然两者都可以使用一行。
```
// 可接受的
var baz = ( true === conditionalStatement() ) ? 'thing 1' : 'thing 2';

// 更好的
var baz = firstCondition( foo ) && secondCondition( bar ) ?
    qux( foo, bar ) :
    foo;

```
当一个条件判断在一行中过长，就必须在body内换行且缩进一个等级以此来区分。
```
if ( firstCondition() && secondCondition() &&
        thirdCondition() ) {
    doStuff();
}

```

#### 链接方法调用
当一个链接方法的调用在一行中过长，那就必须一行调用一个，在对象的调用的方法的一个单独的行的第一次调用。如果方法改变了上下文，就必须使用一个额外的缩进。
```
elements
    .addClass( 'foo' )
    .children()
        .html( 'hello' )
    .end()
    .appendTo( 'body' );

```

#### 全局变量的操作
### var声明变量
每个函数应该开始于一个单独var语句来声明任何必要的局部变量。如果一个函数没有使用var来声明变量，变量就会泄露到外部范围（通常是一个全局变量，最糟糕的一种情况），并且可以导致意外的引用和修改数据。

var语句下的操作应该列入到个别行，尽管声明可以被组织成一个单行。任何额外的行应该用一个额外的tab来缩进。对象和函数如果占据了太多行就该被设计在var语句之外，来避免过度缩进。
```
// 好的
var k, m, length,
    // 用一个tab缩进后来的行
    value = 'WordPress';

// 不好的
var foo = true;
var bar = false;
var a;
var b;
var c;

```

#### 全局变量
在过去，wordpress核心更重的使用全局变量。自从核心JS文件有的时候被用于插件，已经存在的全局变量不应该被移除。

所有在一个文件下使用的全局变量应该在文件的顶部备注。多个全局变量可以用逗号隔开。

这个例子在文件中备注了```passwordStrength```可用全局变量:
> / * global passwordStrength:true * /

这个```true```值意味着```passwordStrength```正在这个文件下定义。如果你访问了一个在其他地方定义的全局变量，省略```:true```来指定全局变量为只读。

#### 通用库
Backbone, jQuery,Underscore,和```wp```全局对象在```.jshint```文件根目录中都注册为可用的全局变量。
Backbone和Underscore在任何时候可以直接访问，jQuery应该通过```$```来访问在传递一个```jQuery```对象到一个匿名函数的时候:
```
(function( $ ) {
  // Expressions
})( jQuery );

```
这将否定```.noConflict```调用的必要，或者使用另一个变量时设置```$```。
为```wp```对象添加或修改的文件必须安全的访问全局以避免重写之前的属性设置。
```
// 在文件的顶部，设置已存在的“wp”的值(如果存在)
window.wp = window.wp || {};

```

#### 命名规范
变量和函数的命名应该用完整的单词，使用驼峰式命名，第一个字母小写。这里面写了与这个标准的不同之处[WordPress PHP coding standards](https://make.wordpress.org/core/handbook/best-practices/coding-standards/php/#naming-conventions).

使用```use```的构造函数都应该首字母大写(UpperCamelCase).

名字应该是具有描述性的，但是不要过度。遍历是允许异常的，比如在一个循环中使用```i```来代表索引。、

#### 注释
注释出现在调用它们的代码之前，且应该始终以空白行开头。将注释的首字母大写，并且当编写一个完整的句子的时候在末尾包含一个句号.在注释标记和注释内容之间应该是一个空格。
单行注释:
```
someStatement();

// Explanation of something complex on the next line
$( 'p' ).doSomething();

```
多行注释应该用在长注释，参见[JavaScript Documentation Standards](https://make.wordpress.org/core/handbook/best-practices/inline-documentation-standards/javascript/#multi-line-comments):
```
/*
 * This is a comment that is long enough to warrant being stretched
 * over the span of multiple lines.
 */

```

行内注释是一个例外当用于在格式化参数列表中作特殊参数注解的时候:
```
function foo( types, selector, data, fn, /* INTERNAL */ one ) {
    // Do stuff
}

```

#### 等式
严格模式的检查等式(===)通常优于抽象模式的检查等式(==),只有一个例外就是当通过检查对象```null```检查是为```undefined```还是为```null```的时候。
```
// 检查undefined和Null值，处于某些重要原因
if ( undefOrNull == null ) {
    // Expressions
}

```

#### 类型检查
这些是对象的类型检查的最佳的方法:
- String: ```typeof object === 'string'```
- Number: ```typeof object === 'number'```
- Boolean: ```typeof object === 'boolean'```
- Object: ```typeof object === 'object' or _.isObject( object )```
- Plain Object: ```jQuery.isPlainObject( object )```
- Function: ```_.isFunction( object) or jQuery.isFunction( object )```
- Array: ```_.isArray( object ) or jQuery.isArray( object )```
- Element: ```object.nodeType or _.isElement( object )```
- null: ```object === null```
- null or undefined: ```object == null```
- undefined:
 - Global Variables: ```typeof variable === 'undefined'```
 - Local Variables: ```variable === undefined```
 - Properties: ```object.prop === undefined```
 - Any of the above: ```_.isUndefined( object )```

无论何处，Backbone或者Underscore是随时可用，你被鼓励使用[Underscore.js](http://underscorejs.org/#isElement)的类型检查方法，比jquery更好。

#### 字符串
对字符串文字使用单引号:
```
var myStr = 'strings should be contained in single quotes';

```
当一个字符串包含单引号，它们需要用反斜杠隔开```\```:
```
// 隔开字符串下的单引号:
'Note the backslash before the \'single quotes\'';
```

#### switch语句

```switch``` 语句通常是不推荐使用的，但是当有大量的case的时候它变得有用了，尤其是当多个case被同个块使用的时候。或者通过逻辑(默认的情况)可以使用时

当使用```switch```语句:
- 在每个case后换行，当允许的语句崩溃时，请显式的注释
- 在```switch```语句中用一个tab来缩进每个case
```
switch ( event.keyCode ) {

    // ENTER and SPACE both trigger x()
    case $.ui.keyCode.ENTER:
    case $.ui.keyCode.SPACE:
        x();
        break;
    case $.ui.keyCode.ESCAPE:
        y();
        break;
    default:
        z();
}
```

不推荐从一个switch语句中返回一个值:
使用```case``` 块来设置值，然后在末尾返回哪些值。

```
function getKeyCode( keyCode ) {
    var result;

    switch ( event.keyCode ) {
        case $.ui.keyCode.ENTER:
        case $.ui.keyCode.SPACE:
            result = 'commit';
            break;
        case $.ui.keyCode.ESCAPE:
            result = 'exit';
            break;
        default:
            result = 'default';
    }

    return result;
}

```

#### 最佳实践

数组
在javascript中创建数组应该使用[]表示法来构造比```new Array()```更好
```
var myArray = [];

```
你可以在构造期间初始化一个数组
```
var myArray = [ 1, 'WordPress', 2, 'Blog' ];

```
在javascript中，定义关联数组作为对象。

对象
在javascript中有很多方法来创建对象，对象文本标记，```{}```。是既高效，又容易阅读的。
  ```
  var myObj = {};

  ```
  应该使用对象文本标记除非对象请求的是一个特定的原型，在这种情况下应该用一个```new```引用的构造函数来创建对象。
```
var myObj = new ConstructorMethod();

```
对象的属性应该通过点符号来访问，除非值是一个变量，一个[ reserved word](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords)(关键字)，或者一个不会被有效识别的字符串。
```
prop = object.propertyName;
prop = object[ variableKey ];
prop = object['default'];
prop = object['key-with-hyphens'];

```

#### 尤达条件
为了[ PHP code standards](https://make.wordpress.org/core/handbook/best-practices/coding-standards/php/#yoda-conditions)的一致性，当你在比较将对象跟一个字符串，布尔值，整形或者其他常量或者文字比较时，变量应该放在右边，常量或者文字应该放在左边。
```
if ( true === myCondition ) {
    // Do stuff
}
```
"读起来有点奇怪，习惯它吧，你会的"

#### 遍历
当使用```for```循环遍历一个大型集合时，推荐做法是将循环的最大值存为一个变量好过每次重新计算:
```
// 好的并且高效
var i, max;

// getItemCount() gets called once
for ( i = 0, max = getItemCount(); i < max; i++ ) {
    // Do stuff
}

// 不好的并且效率低下
// getItemCount() gets called every time
for ( i = 0; i < getItemCount(); i++ ) {
    // Do stuff
}

```

#### Underscore.js 集合函数
学习并弄懂Underscore的[ collection and array methods](http://underscorejs.org/#collections)(集合和数组方法)。这些函数，包含了```_.each```, ```_.map```,```_.reduce```,允许对大数据集的高效的，可读的转换。
Underscore也允许jQuery-style链接普通的js对象：
```
var obj = {
    first: 'thing 1',
    second: 'thing 2',
    third: 'lox'
};

var arr = _.chain( obj )
    .keys()
    .map(function( key ) {
        return key + ' comes ' + obj[ key ];
    })
    // Exit the chain
    .value();

// arr === [ 'first comes thing 1', 'second comes thing 2', 'third comes lox' ]

```

#### jquery集合的遍历

遍历一个jquery对象的集合的时候应当使用jquery方法来遍历
```
$tabs.each(function( index, element ) {
    var $element = $( element );

    // Do stuff to $element
});
```
绝对不要使用jquery来遍历一些不成熟的数据或者vanilla js对象。

#### JSHint
[JSHint](http://jshint.com/)是一种自动化保证代码质量的工具，用于捕获JavaScript代码中的错误。在WordPress开发中使用了JSHint，以快速验证补丁没有将任何逻辑或语法错误引入前端。

### 安装和运行JSHint
JSHint是通过使用一个叫[Grunt](https://gruntjs.com/)的工具来运行，这两个项目都被写进了[Node.js](https://nodejs.org/en/).WordPress代码开发自带的配置文件可以让安装和配置这些工具变得更简单。
为了安装 Node.js，点击这个安装连接[Node](https://nodejs.org/en/)网页，你要下载针对你的系统的正确的安装文件，跟着安装步骤来安装项目。

一旦安装了Node.js，打开命令行窗口,进入到[wordpress svn](https://make.wordpress.org/core/handbook/tutorials/installing-wordpress-locally/from-svn/)副本仓库(使用```cd ~/directoryname```). 你应该在包含了```package.json```文件的项目根目录下了.

下一步，在命令行窗口输入```npm install```。这将会下载和安装所有wordpress用到的Node包。

最终，输入```npm install -g grunt-cli```来安装Grunt命令行接口(CLI)包。Grunt CLI是用来在wordpress中执行并运行Grunt任务的。

你现在应该可以输入```grunt jshint```来检查所有wordpress 的JS文件的语法和逻辑错误。如果为了仅仅检测核心代码，输入```grunt jshint:core```;为了单元测试某个.js文件，输入```grunt jshint:tests```.

JSHint 设置
JSHint的配置选项在wordpress svn苍鹭中的一个[.jshintrc ](https://develop.svn.wordpress.org/trunk/.jshintrc)文件
中存储，这文件定义了JSHint能在wordpress源代码中找到什么样的错误。

目标一个文件
用JSHint来检查一个指定的文件，在命令的末尾添加```--file=filename.j```。例如，这个例子仅仅检查在wordpress核心JS文件中文件名为"admin-bar.js"。
```
grunt jshint:core --file=admin-bar.js
```
还有这个仅会在项目的单元测试下检查“password-strength-meter.js”
```
grunt jshint:tests --file=password-strength-meter.js
```
当你仅仅修改了一两个指定文件的时候，并且不想消耗JSHint运行处理很多文件所等待的时间，这个JSHint指定单文件的做法就是很有用的。

#### JSHint Overrides: Ignore Blocks
某些情况下，JSHint应该排除一个文件中的某些部分。举个例子，工具栏中的脚本文件包含了jQuery HoverIntent插件的简化代码-这是不应该通过JSHint的第三方代码，即使它是WordPress核心JavaScript文件的一部分。
为了排除一个JSHint正在处理的指定文件范围，将其包含在JSHint的指令注释中:
```
/* jshint ignore:start */
if ( typeof jQuery.fn.hoverIntent === 'undefined' ) {
    // hoverIntent r6 - Copy of wp-includes/js/hoverIntent.min.js
    (function(a){a.fn.hoverIntent=...............
}
/* jshint ignore:end */
```

#### 鸣谢
jquery的案例是改编自[jQuery JavaScript Style Guide](https://contribute.jquery.org/style-guide/js/),这是在MIT的许可下提供的.
