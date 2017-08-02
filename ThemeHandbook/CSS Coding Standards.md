#### css编码标准
像任何编码标准那样，wordpressCSS的编码标准的目的是为了给那些在wordpress开源项目和社区中在多方面中合作和评审的时候提供一个标准，从核心代码到主题，到插件，一个项目下的文件应该看起来像由一个人来写的。除此之外，要具备可读性，有意义的，一致的优雅的创建代码。

在核心stylesheets下，经常会发现矛盾。我们正致力于解决这些问题，并且尽一切努力来在这点上进行补丁和提交以遵循CSS编码标准。以上的更多信息以及对UI/前端开发有用的会在另一个开发手册中讲到。

#### 结构
有很多不同的方法来组织一个样式表。以CSS为核心，保持一个高辨识度是非常重要的。这确保了后来的开发贡献者们能清楚的理解文档的流程。
- 使用tab键，不要用空格来缩进每个属性。
- 不同的节段之间添加两个空白行并且在同一个节段的不同的块之前添加一个空白行。
- 每个选择器应该独占一行，以一个逗号或者一个开始花括号来结尾。属性-值对应该独占一行，值跟属性之间应有一个tab缩进，并且以分号结束。结束花括号应该左对齐，使用相同缩进像选择器开始那样。

规范的
```
#selector-1,
#selector-2,
#selector-3 {
    background: #fff;
    color: #000;
}
```
不规范的
```
#selector-1, #selector-2, #selector-3 {
    background: #fff;
    color: #000;
    }

#selector-1 { background: #fff; color: #000; }
```

#### 选择器
在某些特定情况下，为了更好的响应式，众多的选择器让我们变得更高效，但是如果不经测试就会有与预料相反的结果。特指选择器可以让我们节约时间，但是很快让样式表变得杂乱。运用你最好的判断力来创建选择器，在全部样式和布局之间找到正确的平衡。
- 类似针对文件名的[ WordPress PHP Coding Standards](https://make.wordpress.org/core/handbook/best-practices/coding-standards/php/#naming-conventions)命名规范，在命名选择器的时候使用小写的字母和连字符，避免下划线和驼峰式命名。
- 使用可读性强，能描述他们修饰的元素的选择器。
- 属性选择器应该在值的两边使用双引号。
- 避免使用过于仔细的选择，比如```div.container```可以简化成``` .container```

规范的
```
#comment-form {
    margin: 1em 0;
}

input[type="text"] {
    line-height: 1.1;
}
```

不规范的
```
#commentForm { /* 避免驼峰式命名 */
    margin: 0;
}

#comment_form { /* 避免下划线 */
    margin: 0;
}

div#comment_form { /* 避免过于严格 */
    margin: 0;
}

#c1-xr { /* 什么是c1-xr?! 用一个更好，更具有意义的名字. */
    margin: 0;
}

input[type=text] { /* 应该像这样 [type="text"] */
    line-height: 110% /* 这里有两个错误，1不要用百分号应该用1.1。2没有分号 */
}
```

#### 属性
类似于选择器，在使用过于具体的属性的时候会阻碍设计的灵活性。少即是多，确保你没有重复写样式和引入固定模式(当一个流体方案具有更强的适应性);
- 属性应该遵循一个冒号和一个空格。
- 所有属性和值应该小写，除了font名和一些特定属性之外。
- 颜色使用16进制代码，或者rgba()当需要设置opacity的时候。避免RBG格式和大写，并且尽量缩写:用```#fff```来代替```#FFFFFF```。
- 使用缩写法(当重写样式的时候例外)，在使用background,border,font,list-style,margin和padding这些属性的值得时候。(关于缩写法，看[ CSS Shorthand](https://codex.wordpress.org/CSS_Shorthand))
规范的
```
#selector-1 {
	background: #fff;
	display: block;
	margin: 0;
	margin-left: 20px;
}
```
不规范的
```
#selector-1 {
	background:#FFFFFF;
	display: BLOCK;
	margin-left: 20PX;
	margin: 0;
}
```
#### 属性排序
```
“Group like properties together, especially if you have a lot of them.”
— Nacin
```
除此之外，在某些方式下你需要选择一些更有语义化的东西来满足语义化。随机排序是不好的，不是优雅的。在wordpress核心中，我们的选择是合乎逻辑和有序组织的，那些通过语义化组织的属性并且按以下分类排序的。按下面组织的属性在不同的区域中创建过渡的时候是有战略意义的。就像color之前定义background,这是排序的标准:
- Display
- Positioning
- Box model
- Colors and Typography
- Other

那些还没用到的核心本身，比如CSS3动画，或许没有像上面那样但是有可能以一个合乎逻辑的方式来融入，随着CSS的发展，我们的标准也会随之变动。

Top/Right/Bottom/Left (TRBL/trouble) 应该为任何相关的属性而排序，就像值的排列顺序一样。例如```border-radius-*-*```应该是top-left, top-right, bottom-right, bottom-left. 这是从值的缩写法的排序中衍生而来的。

例子
```
#overlay {
    position: absolute;
    z-index: 1;
    padding: 10px;
    background: #fff;
    color: #777;
}
```
另外一个经常用的方法，被Automattic/WordPress.com主题团队所使用的，就是不管有没有例外都按字母顺序来排序属性。
```
#overlay {
    background: #fff;
    color: #777;
    padding: 10px;
    position: absolute;
    z-index: 1;
}
```

#### 前缀
在2/13/2014更新，[ [27174]](https://core.trac.wordpress.org/changeset/27174)之后
我们使用[ Autoprefixer](https://github.com/postcss/autoprefixer)作为一个预处理工具来方便管理必要的浏览器前缀。因此，这个部分的内容大部分是毫无意义的。对于那些对不通过grunt来输出感兴趣的人来说，前缀应该是从长到短。所有其他的间距遵循标准的剩余部分。
```
.sample-output {
    -webkit-box-shadow: inset 0 0 1px 1px #eee;
    -moz-box-shadow: inset 0 0 1px 1px #eee;
    box-shadow: inset 0 0 1px 1px #eee;
}
```
#### 值
这里有多种方式来输入属性的值，遵循以下的手册来帮助我们保持高度的一致性。
- 值之前空格，冒号。
- 不用空格来填充括号。
- 总是以冒号来结尾。
- 使用双引号代替单引号，并且仅在需要的时候使用，像font名字有空格的时候
- font weight应该使用数字类型值来定义。(比如，400代替normal，700代替bold)。
- 0 值应该不要存在单位除非必要的话，比如transion-duration.
- line-height也应该是无单位。除非必要的时候比如定义指定像素值。 这不仅仅是一个样式的惯例，但是这里值得注意。更多信息:[http://meyerweb.com/eric/thoughts/2006/02/08/unitless-line-heights/](http://meyerweb.com/eric/thoughts/2006/02/08/unitless-line-heights/)。
- 使用带小数点的数字型值，包括rgba();
- 在一个属性有多个逗号隔开的值的时候应该通过一个空格或者新的一行来隔开，包括rgba().新的一行应该用于更长的多出来的那部分的值。比如这些box-shadow,text-shadow使用缩写法的属性。每个比最初后来的值
应该在新的一行上，就像选择器缩进，以上一个值来进行左对齐。

规范的
```
.class { /* 引号正确用法 */
    background-image: url(images/bg.png);
    font-family: "Helvetica Neue", sans-serif;
    font-weight: 700;
}

.class { /* 0值的正确使用 */
    font-family: Georgia, serif;
    line-height: 1.4;
    text-shadow: 0 -1px 0 rgba(0, 0, 0, 0.5),
                 0 1px 0 #fff;
}
```

不规范的
```
.class { /* 避免没有空格和分号 */
    background:#fff
}

.class { /* 避免在0值的时候加入单位 */
    margin: 0px 0px 20px 0px;
}

.class {
    font-family: Times New Roman, serif; /* 当引用Font名的时候使用引号 */
    font-weight: bold; /* 避免这种形式，应该使用数字值 */
    line-height: 1.4em;
}
```

#### 媒体查询
媒体查询允许我们在不同的屏幕尺寸下优雅的降低我们的DOM操作。如果你使用了这个功能，一定要在你选择的断点上进行测试。
- 通常明智的做法是在stylesheet底部组织媒体查询
  - 一个因wp-admin.css文件引起的异常，由于它非常大并且每个部分基本上代表了各自的一个样式表。媒体查询因此尽可能添加在适当的部分的底部。

- 媒体查询的规则集应该一级缩进。

```
@media all and (max-width: 699px) and (min-width: 520px) {

        /* Your selectors */
}

```
#### 评论
- 评论和注释。如果涉及到文件尺寸，利用压缩文件和SCRIPT_DEBUG常量。长评论应该被限制在80个字符长度以内。
- 目录表应该用于长stylesheets，由于这些高度划分。使用索引数字(1.0,1.1,2.0,等等)帮助来搜索和跳转到一个位置。
- 注释应该被格式化成像PHPDoc那样。[CSSDoc](https://make.wordpress.org/core/handbook/best-practices/coding-standards/css/)标准不是必要的，广泛的被接收或者使用除了某些方面随着时间的推移以后可能会被采用。Section/subsection的header应该前后都有空白行。在一段与之关联的行内注释中不应该有空白行。

For sections and subsections:
```
/**
* #.# 区域标题
*
* 区域的描述，是否使用了媒体查询等等
*/

.selector {
    float: left;
}
```

For inline:
```
/* 这是一个关于选择器的注释 */
.another-selector {
    position: absolute;
    top: 0 !important; /* 我应该解释这里为什么使用!important */
}
```

#### 最佳实践
样式表会慢慢变长。当目标开始重复和重叠的会后，注意力慢慢消失。从一开始写聪明的代码会帮助我们在重新审查的时候保持变更的灵活性。
- 如果你企图修复一个问题，尝试在添加更多之前移除部分代码。
- 奇怪的数字是不好的，这些数字用于快速修复，一次性的。比如:```
.box { margin-top: 37px }``` .
- DOM每次都会变，将你想使用的元素作为目标而不是通过它的父元素。比如，使用```.highlight```而不是```.highlight a``` (当选择器在父节点上)
- 知道何时使用height属性，它应该被用于当你引用外部元素的时候(比如images)。另一方面为了灵活性使用line-height。
- 不要重新修改默认属性&值组合(比如display:block;在块级元素上。)
