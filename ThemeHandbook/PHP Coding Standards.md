#### PHP编码标准
PHP标记的WordPress代码结构的某些部分在样式上是不一致的。wordpress致力于提升用户保持一致性的样式，这样代码就会变得干净并且容易阅读，一目了然。

在wordpress中编写PHP代码的时候记住下面这些要点，是否为核心程序的代码，插件或者主题。该指南在许多方面类似于[Pear standards](http://pear.php.net/manual/en/standards.php),但是某些关键方面不同。
参见:[PHP Documentation Standards](https://make.wordpress.org/core/handbook/best-practices/inline-documentation-standards/php/)(php文档标准)

#### php
##### 单引号和双引号
适当使用单引号和双引号。如果你没有在字符串中求值，使用单引号。你几乎应该不会避开在字符串中使用引号，因为你可以替换你的引用风格，像这样:
```
echo '<a href="/static/link" title="Yeah yeah!">Link name</a>';
echo "<a href='$link' title='$linktitle'>$linkname</a>";
```

属性当中的文本应该通过```esc_attr()```来运行，这样单引号或者双引号不会结束属性的值，并且使HTML无效，引起安全问题。进一步的详细信息参见[ Data Validation](https://codex.wordpress.org/Data_Validation)

#### 缩进
你的缩进应该总是反映逻辑结构。使用tab而不是空格，因为要考虑客户之间的灵活性。
例外：如果你有通过空格能更具可读性的代码
```
[tab]$foo   = 'somevalue';
[tab]$foo2  = 'somevalue2';
[tab]$foo34 = 'somevalue3';
[tab]$foo5  = 'somevalue4';
```
对于关联数组，值应该开始于新的一行，注意到最后一个数组的子项之后的逗号；这是推荐使用的因为它更容易改变数组的排序，并且在加入新的项目的时候让其更简洁。
```
$my_array = array(
[tab]'foo'   => 'somevalue',
[tab]'foo2'  => 'somevalue2',
[tab]'foo3'  => 'somevalue3',
[tab]'foo34' => 'somevalue3',
);
```
针对```switch```结构``case```应该用一个tab缩进，在```switch```语句中的```case```语句中```break```应该用一个tab缩进。
```
switch ( $type ) {
[tab]case 'foo':
[tab][tab]some_function();
[tab][tab]break;
[tab]case 'bar':
[tab][tab]some_function();
[tab][tab]break;
}
```
经验法则:在行的开始处要使用tabs，而空格可以用在行内对齐。

#### 大括号样式
这里显示的所有块都是用了大括号:
```
if ( condition ) {
    action1();
    action2();
} elseif ( condition2 && condition3 ) {
    action3();
    action4();
} else {
    defaultaction();
}
```
如果你有一个长的块，考虑一下是否可以拆分成两个甚至更多的小的块，函数，或者方法。这是为了降低复杂度，让测试更简单，提升可读性。

应该经常使用大括号，甚至那些不必要使用的时候:
```
if ( condition ) {
    action0();
}

if ( condition ) {
    action1();
} elseif ( condition2 ) {
    action2a();
    action2b();
}

foreach ( $items as $item ) {
    process_item( $item );
}
```

值得注意的是需要使用括号，这意味着禁止使用单语句的内联控制结构。你可以自由使用[alternative syntax for control structures](http://php.net/manual/en/control-structures.alternative-syntax.php)(```if```,```endif```,```while```,```endwhile```)--尤其是在HTML中嵌入的PHP代码的模板，举个例子:
```
<?php if ( have_posts() ) : ?>
	<div class="hfeed">
		<?php while ( have_posts() ) : the_post(); ?>
			<article id="post-<?php the_ID() ?>" class="<?php post_class() ?>">
				<!-- ... -->
			</article>
		<?php endwhile; ?>
	</div>
<?php endif; ?>
```
#### 用```elseif```,而不是```else if```
在```if|elseif```语句中使用```else if```是不兼容冒号语法的，所以在条件判断语句中使用```elseif```。

#### 正则表达式
Perl兼容的正则表达式(PCRE、preg函数)应该优先于它们的POSIX对等项。不要使用```/e```switch,使用```preg_replace_callback```代替。

对于正则表达式，使用单引号是最方便的，与双引号字符串相反，他们仅仅只有```\'```和```\\```

#### PHP标签的开始和闭合
当在HTML块中嵌入多行PHP片段，php的开始和闭合标签必须独占一行。
正确的(多行)
```
function foo() {
    ?>
        <div>
        <?php
        echo bar(
            $baz,
            $bat
        );
        ?>
        </div>
    <?php
}
```
正确的(单行)
```
<input name="<?php echo esc_attr( $name ); ?>" />

```
不正确:
```
if ( $a === $b ) { ?>
<some html>
<?php }
```

#### 不要省略PHP标签
重要:绝对不要使用省略的PHP标签。总是使用完整的PHP标签。
正确:
```
<?php ... ?>
<?php echo $var; ?>
```
不正确:
```
<? ... ?>
<?= $var ?>

```

#### 移除后面多余的空格
在每行代码的末尾不要有空格，推荐在一个文件的末尾省略掉PHP闭合标签。如果你使用标签，请确保后面的多余的空格。

#### 空格用法
总是在逗号之后使用空格，还有在逻辑，比较，字符串和运算操作的两边。
```
x == 23
foo && bar
! foo
array( 1, 2, 3 )
$baz . '-5'
$term .= 'X'
```

在插入```if```,```elseif```,```foreach```,```for```,```switch```语句时的小括号的开始和闭合两边用空格。
```
foreach ( $foo as $bar ) { ...
```
定义一个函数的时候，这样做：
```
function my_function( $param1 = 'foo', $param2 = 'bar' ) { ...
```
当调用一个函数的时候，这样做:
```
my_function( $param1, func_param( $param2 ) );
```
使用逻辑比较的时候，这样做:
```
if ( ! $foo ) { ...
```
指定类型的时候，这样做:
```
foreach ( (array) $foo as $bar ) { ...

$foo = (boolean) $bar;
```
当数组子项使用变量的时候，在变量两边加上空格，比如:
```
$x = $foo['bar']; // correct
$x = $foo[ 'bar' ]; // incorrect

$x = $foo[0]; // correct
$x = $foo[ 0 ]; // incorrect

$x = $foo[ $bar ]; // correct
$x = $foo[$bar]; // incorrect
```
在一个switch语句中，一个case语句的冒号之前不能有空格。
```
switch ( $foo ) {
    case 'bar': // correct
    case 'ba' : // incorrect
}

```

#### SQL语句的格式化
在格式化SQL语句时，如果它足够复杂，可以将它分成几行和缩进。大部分语句都可以通过一行搞定。部分SQL语句像```UPDATE```或者```WHERE```总是大写。

更新数据库的函数应该期望在传递他们的参数时缺少SQL语句的转义，转义应该尽可能接近查询时间。使用```$wpdb->prepare()```更好。

``` $wpdb->prepare() ```是一个SQL查询中用于处理转义，引用，整形转换的方法。它使用了```sprintf()```格式化样式中的一个子集。比如:

```
$var = "dangerous'"; // raw data that may or may not need to be escaped
$id = some_foo_number(); // data we expect to be an integer, but we're not certain

$wpdb->query( $wpdb->prepare( "UPDATE $wpdb->posts SET post_title = %s WHERE ID = %d", $var, $id ) );
```

```%s``` 是字符串类型参数，```%d```是整形参数。注意，他们不是被引用的！```$wpdb->prepare()```将会为我们提供转义和引用。这是有好处的，这样我们就不用记住手动使用```[esc_sql()](https://codex.wordpress.org/Function_Reference/esc_sql)```，而且是否有东西溢出一目了然，因为当查询发生时它就正确执行了。

点击[Data Validation](https://codex.wordpress.org/Data_Validation)查看更多信息

#### 数据库查询
避免直接操作数据库。如果你需要得到数据就定义一个函数，使用它，数据库抽象(使用函数代替查询)将会帮助你的代码的正向兼容，在缓存机制下，这样会快很多。

如果你必须操作数据库，通过发送消息给[ wp-hackers mailing list](https://codex.wordpress.org/Mailing_Lists#Hackers)来给这些开发者。他们可能会想到考虑创建一个函数在下一个wordpress版本中来实现你想要的功能。

#### 命名规范
在变量，操作，函数命名的时候全部使用小写字母(不要用驼峰命名)。用下划线隔开，无非必要的时候不要缩写变量名。让代码变得更清晰和描述性。
```
function some_name( $some_variable ) { [...] }
```
类名应该使用下划线隔开，首字母大写。
```
class Walker_Category extends Walker { [...] }
class WP_HTTP { [...] }
```
常量应该全部大写，且可以用下划线隔开。
```
define( 'DOING_AJAX', true );
```
这个文件命名规范适用于所有带有类的当前的或者新的文件。有个例外情况的三个包含了代码的文件，class.wp-dependencies.php, class.wp-scripts.php, class.wp-styles.php，被移植到了BackPress.
这些文件是用```class.```预先准备的。在class后面的点不是连字符。

在```wp-includes```中文件包含了模板标签，应该在名字的最后面加上```-template```,这样意思就更明显了。
```
general-template.php
```

#### 函数参数的值的自我解释性
在调用函数时更喜欢字符串类型的值而不是```true```和```false```。
```
// 不正确的
function eat( $what, $slowly = true ) {
...
}
eat( 'mushrooms' );
eat( 'mushrooms', true ); // true是什么意思?
eat( 'dogfood', false ); // false是什么意思，true的反义词吗？
```
自从PHP不支持命名参数后，值的意思变得不可捉摸，而且每次我们想像上面的例子那样通过调用函数，我们就必须去搜索函数的定义，这代码如果使用可描述性的字符串来代替布尔类型的值的话就更具可读性。
```
// 正确
function eat( $what, $speed = 'slowly' ) {
...
}
eat( 'mushrooms' );
eat( 'mushrooms', 'slowly' );
eat( 'dogfood', 'quickly' );
```
当函数参数需要更多的描述性单词的时候，```$args```数组也许是一个更好的做法
```
// Even Better
function eat( $what, $args ) {
...
}
eat ( 'noodles', array( 'speed' => 'moderate' ) );
```

#### 动态钩子函数命名的插补
动态钩子应该使用插补来命名，好过以可读性和可发现性为目的的联合。

动态钩子是在他们标签名中包含了动态值的钩子。比如```{$new_status}_{$post->post_type}``` (publish_post)

在钩子标签中使用的变量应该用成对的大括号```{```,```}```包裹,在完整的标签名外使用双引号。这样确保PHP可以正确的解析内插字符串中给定的变量的类型。
```
do_action( "{$new_status}_{$post->post_type}", $post->ID, $post );

```
可能的情况下，标签名中的动态值尽可能的简洁。```$user_id```比```$this->id```更有自我描述性。

#### 三元操作符
[Ternary](Ternary)操作符是好用的，但总是会测试语句是否为true。另一方面，它会让人迷惑(使用```! empty()```例外，因为这里的错误测试通常更直观)。

比如：
```
// (if statement is true) ? (do this) : (else, do this);
$musictype = ( 'jazz' == $music ) ? 'cool' : 'blah';
// (if field is not empty ) ? (do this) : (else, do this);
```

#### 尤达条件
```
if ( true == $the_force ) {
    $victorious = you_will( $be );
}
```
当逻辑比较涉及到变量的时候，总是将变量放到右边，然后将常量，文本，或者调用函数在左边。如果两边都不是变量，这个排序就不重要了。(在[ computer science terms](https://en.wikipedia.org/wiki/Value_(computer_science)#Assignment:_l-values_and_r-values),在比较中总是尝试将l值放右边，r值放左边)

在上面的例子中，如果你省略一个等于号(认了吧，在我们这些老手身上也会发生)，你会得到一个语法错误，因为你不能给一个像```true```的常量赋值。如果是```( $the_force = true )```周围的语句，操作将会完美有效的，返回```1```,导致if语句的值为```true```，然后你会花点时间来找这个bug。

读起来有点奇怪，习惯它吧，你会的。

这个适用于==,!=,===,!==。<, >, <= or >= 尤达条件是相当难以阅读的，所以最好尽量避免。

#### 巧妙代码
总的来说，可读性比巧妙性，简洁性更重要。
```
isset( $var ) || $var = some_function();
```
尽管上面的代码很巧妙，但是如果你不熟悉它的话就需要花点来懂它。所以，要这样写:
```
if ( ! isset( $var ) ) {
    $var = some_function();
}
```
在一个```switch```语句中，可以在一个公共块里有多个空的case。
如果一个case包含了一个块，然后传递到下一个块，无论如何，这样就必须要注释清除。
```
switch ( $foo ) {
    case 'bar':       // Correct, an empty case can fall through without comment.
    case 'baz':
        echo $foo;    // Incorrect, a case with a block must break, return, or have a comment.
    case 'cat':
        echo 'mouse';
        break;        // Correct, a case with a break does not require a comment.
    case 'dog':
        echo 'horse';
        // no break   // Correct, a case can have a comment to explicitly mention the fall through.
    case 'fish':
        echo 'bird';
        break;
}
```

#### 错误控制操作符@
如[PHP docs](http://www.php.net//manual/en/language.operators.errorcontrol.php)所述:

> PHP支持一个错误控制操作符，at符号(@).当考虑到PHP中的表达式，任何由表达式产生的错误信息都将被忽略。

尽管在核心中已经存在这个操作符，它通常被惰性地使用而不是进行适当的错误检查。非常不鼓励使用它，甚至php文档也声明:
> 警告:当前，“@”错误控制操作符前缀甚至会禁用错误报告，这些错误报告将会终止脚本的执行。此外，这意味着如果您使用“@”来抑制某个函数的错误，或者它是不可用的，或者已经出现了错误，那么这个脚本就会在这里死去，没有任何提示说明原因。

#### 不要```extract()```
按照[#22400](https://core.trac.wordpress.org/ticket/22400)
```
extract()是一个糟糕的函数，它使代码更难调试，更难理解。我们应该阻止它的使用，并去除它的所有用途。
约瑟夫斯科特很好地解释了为什么它是坏的[ a good write-up of why it’s bad](https://blog.josephscott.org/2009/02/05/i-dont-like-phps-extract-function/)。
```

#### 鸣谢
- PHP标准:[Pear standards](http://pear.php.net/manual/en/standards.php)

#### 主要改动
- 2013年11月13日，大括号应该总是被使用，即使没必要用它们的时候。[Braces should always be used, even when they are optional](https://make.wordpress.org/core/2013/11/13/proposed-coding-standards-change-always-require-braces/)
- 2014年10月20日，更新了大括号的用法预示着控制结构的交替语法是被允许的，甚至是鼓励的。单行行内控制结构是被禁止的。
- 2014年1月21日，添加内容来禁止 extract().
