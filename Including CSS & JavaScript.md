#### css个javascript的引入
在你创建你的主题的时候，你或许想创建额外的stylesheets或者javascript文件，无论如何，请记住在wordpress站点中不仅仅激活的主题需要，许多不同的插件页需要用到css和JS。这样一来每个工作都很和谐。在主题和插件引入脚本和样式表的时候使用标准的wordpress方法是非常重要的。这会保证网页保持高效并且不会有兼容性问题。

wordpress加入scripts和styles是相当简单的过程。本质上，你将会创建一个排列你所有的scripts和styles的函数。当排列一个script或一个style的时候，wordpress创建一个句柄和路径来搜索你的文件，并且有可能有任何依赖(像jquery)，然后你会用一个钩子来插入你的scripts和styles。

#### 排列scripts和styles
往你的主题加入scripts和styles适当的方式就是在functions.php文件中排列它们。style.css文件是所有主题都需要的，但也许需要加入其它文件来扩展你的主题的功能。

> wordpress会包含许多js文件作为软件包的一部分，包括常用的库如jquery。在加入你自己的JS文件之前，检查你是否可以使用一个内置的库。

基本就是:
- 1.使用wp_enqueue_script()或者wp_enqueue_style()来排列script或者style.

#### stylesheets
你的css样式表被用于自定义你的主题外观。一个样式表也是一个存储了关于你的主题的信息的一个文件。基于这个原因，style.css文件是每个主题都需要的。

你应该使用wp_enqueue_style来读取样式表，而不是在你的header.php文件中读取它。为了读取你的主要的样式表，你可以在functions.php中排列它。

排列style.css
```
wp_enqueue_style( 'style', get_stylesheet_uri() );
```
这样将会寻找一个名为'style'的样式表并且读取它。
排列一个style的基本函数是:
```
wp_enqueue_style( $handle, $src, $deps, $ver, $media );
```
你可以包含这些参数：
- $handle是样式表的名字
- $src是它的路径，剩下的参数都是可选的。
- $deps决定这个样式表是否依赖于另外一个样式表。如果这个选项被设置，这个样式表将不会被加载除非它所依赖的样式表在最开始已经被加载。
- $ver设置版本号
- $media 可以指定哪种类型的多媒体来读取这个样式表，如'all','screen','print'或者'handheld'。

因此,如果你想在你的主题的根目录下的名为css的文件夹内加载一个名为'slider.css'的样式表，你可以用:
```
wp_enqueue_style( 'slider', get_template_directory_uri() . '/css/slider.css',false,'1.1','all');
```

#### scripts
任何附加的JS文件被一个主题加载的时候应该通过使用wp_enqueue_script。这样确保了适当的加载和缓存，并且允许给目标确定的页面使用条件标签。，它们是可选的。

wp_enqueue_script使用了一个类似wp_enqueue_style的语法。

排列你的script:
```
wp_enqueue_script( $handle, $src, $deps, $ver, $in_footer);
```
- $handle script的名字
- $src script的路径定义
- $deps 你的新script所依赖的任何script的句柄的一个数组。例如jquery。
- $ver 让你列出一个版本号
- $in_footer是一个布尔类型的参数，它允许你将你的Scripts放置在你的html文档的footer里而不是在header中。这样一来它就不会耽搁DOM树的读取。
你的排列函数也许看起来像这样:
```
wp_enqueue_script( 'script', get_template_directory_uri() . '/js/script.js', array ( 'jquery' ), 1.1, true);
```

#### 评论回复script
wordpress评论有相当多的功能，包含了有样式的评论和加强了评论表单。为了评论的正确工作，他们引用了一些script。无论如何，因为他们是需要在js下被定义成确定的选项。评论回复script应该被每个使用到评论的主题添加进去。

包含评论回复正确的方式是使用条件标签来检查是否存在确定的条件。这样一来script就不会在不必要的情况下加载了。例如，你可以仅仅在文章详情页使用is_singular来读取scripts，并且检查确保"Enable threaded comments"选项已被用户选上。所以，你可以设置一个函数像这样:
```
if ( is_singular() && comments_open() && get_option( 'thread_comments' ) ) {
    wp_enqueue_script( 'comment-reply' );
}
```
如果评论被用户启用了，并且我们在一个文章页面，然后评论回复script将会被加载。否则，就不会加载。

#### 排列函数的合并
最好是将所有排列scripts和styles合并成一个单独的函数，然后使用wp_enqueue_scripts来引用它们。这个函数和动作应该放置在下面的初始设置的某处。
```
function add_theme_scripts() {
  wp_enqueue_style( 'style', get_stylesheet_uri() );

  wp_enqueue_style( 'slider', get_template_directory_uri() . '/css/slider.css', array(), '1.1', 'all');

  wp_enqueue_script( 'script', get_template_directory_uri() . '/js/script.js', array ( 'jquery' ), 1.1, true);

    if ( is_singular() && comments_open() && get_option( 'thread_comments' ) ) {
      wp_enqueue_script( 'comment-reply' );
    }
}
add_action( 'wp_enqueue_scripts', 'add_theme_scripts' );
```
#### wordpress包含和注册的默认scripts
默认情况下，wordpress包含了许多网页开发者常用的流行的scripts。同样的scripts也被用于wordpress自身。它们其中的一些被罗列在了下面的清单中。
