#### 主题functions
在wordpress中functions.php文件是你唯一加入功能的地方。它被用于hook成wordpress核心函数以确保你的主题更模块化，更具扩展性，函数性。

#### 什么是functions.php？
functions.php文件行为就像一个wordpress插件，给一个wordpress站点添加功能和特性。你可以通过它来调用wordpress函数和定义你自己的函数。

> 使用一个插件或者functions.php可以产生同样的结果。如果你在创建新的功能的时候不管网页看起来什么样都应该是用到的话,将它们放入一个插件里是最佳实践。

使用wordpress插件或者使用functions.php是有好处的，经过权衡的。

一个wordpress插件:
- 请求指定的，唯一的header文本
- 被存储在wp-content/plugins中，通常在一个子目录内。
- 当激活的时候仅仅在页面加载的时候执行。
- 所有主题都适用
- 应该有一个明确的目的-比如，提供搜索引擎优化功能或者帮助备份。

一个functions.php文件:
- 请求不唯一的header文本
- 被存储在主题的子目录中，在wp-content/themes中
- 仅仅在被激活的主题的文件夹下执行
- 仅应用于主题(如果主题被更改，特性就无法再被使用)
- 为了实现很多不同的功能可以用很多代码块。

每个主题都有自己的functions文件,但是仅仅是被激活的主题的functions.php文件的代码在真正运行。如果你的主题已经有了functions文件，你可以往里面加入代码。如果没有，你可以在你的主题根目录下创建一个纯文本文件命名为functions.php，像下面解释的那样。
一个[child theme](https://developer.wordpress.org/themes/advanced-topics/child-themes/)可以有自己的functions.php文件。为了修改一个父主题，添加一个function到子functions文件中是安全的做法。这样一来，当父主题被更新后，你不用担心添加的最新的function会消失。

> 尽管子主题的functions.php在父主题的functions.php加载之前被wordpress加载.它不会覆盖它，子主题的functions.php可以被用于增强
或者替换父主题的functions。同样的，functions.php在任何插件文件被加载后加载。

通过functions.php你可以:
- 使用wordpress钩子，比如在excerpt_length过滤器下你可以改变你的文章长度(从默认的55个单词)。
- 通过[add_theme_support()](https://developer.wordpress.org/reference/functions/add_theme_support/)来启用wordpress功能。比如，开启文章缩略图，文章形式，和导航菜单。
- 定义你希望在多样的主题模板文件中重用的功能。

> 如果wordpress插件调用了同样的函数，或者过滤器，就像你在你的functions.php中做的那样，会导致不可预期的结果，甚至引起你的网页失效。

#### 实例
以下有些实例，你可以使用它们在你的functions.php文件中来支持多样的功能。这些实例的每一个在你的主题中都被允许如果你选择将它提交到wordpress.org的主题目录下。

#### 主题设置
许多主题功能应该被包含在一个设置功能下，当你的主题被激活的时候就开始运行。如下所示，这些功能的每一个都可以添加到你的functions.php文件里，以此来激活那些被推荐的wordpress功能。

> 使用主题名称来给你的函数命名是重要的。所有实例像下面使用myfirstthemes_这样命名的，都应该基于你的主题名来自定义。

为了创建这个初始化函数，开启一个新函数命名为myfirsttheme_setup(),像这样:
```
if ( ! function_exists( 'myfirsttheme_setup' ) ) :
/**
* Sets up theme defaults and registers support for various WordPress features
*
*  It is important to set up these functions before the init hook so that none of these
*  features are lost.
*
*  @since MyFirstTheme 1.0
*/
function myfirsttheme_setup() {
```
注意:在上面的实例中，myfirsttheme_setup()函数有开始却没有结束。请确保将你的函数结束。

####  自动Feed链接
自动Feed链接使文章和评论的RSS订阅默认可用。这些Feeds将在<head>自动显示。它们可以通过[add_theme_support()](https://developer.wordpress.org/reference/functions/add_theme_support/)来调用
```
add_theme_support( 'automatic-feed-links' );
```

#### 导航菜单
自定义[navigation menus](https://developer.wordpress.org/themes/functionality/navigation-menus/)允许用户在菜单管理面板中来编辑和自定义菜单，给用户提供拖拽接口来在他们的主题中编辑多样的菜单。

你可以在functions.php中设置多样的菜单。他们可以通过使用[register_nav_menus()](https://developer.wordpress.org/reference/functions/register_nav_menus/)来添加，也可以通过使用[wp_nav_menu()](https://developer.wordpress.org/reference/functions/wp_nav_menu/)来插入到一个主题中，这等会在[in this handbook](https://developer.wordpress.org/themes/functionality/navigation-menus/)讨论。如果你的主题要支持多菜单，你应该用一个数组。由于一些主题也许不能自定义导航菜单，为了容易的自定义菜单推荐你使用这个功能。
```
register_nav_menus( array(
    'primary'   => __( 'Primary Menu', 'myfirsttheme' ),
    'secondary' => __( 'Secondary Menu', 'myfirsttheme' )
) );
```

你定义的每一个菜单可以通过使用[wp_nav_menu()](https://developer.wordpress.org/reference/functions/wp_nav_menu/)和使用按theme_location参数所指定的名称来调用。

#### 读取文本域
主题可以被翻译成多语言通过在你的主题中生成用于翻译的字符串。为了做到这一点，你必须使用[load_theme_textdomain()](https://developer.wordpress.org/reference/functions/load_theme_textdomain/).关于主题多语言更多的信息你可以阅读这个[internationalization](https://developer.wordpress.org/themes/functionality/internationalization/).
```
load_theme_textdomain( 'myfirsttheme', get_template_directory() . '/languages' );
```

#### 文章缩略图
[Post thumbnails and featured images ](https://developer.wordpress.org/themes/functionality/featured-images-post-thumbnails/)允许你的用户使用一张图像来代表他们的文章。你的主题可以决定如何来显示它们，依赖于它们的设计。比如，你或许想在每篇文章的归档层显示出post thumbnails(文章缩略图)，又或者你想在你的主页中使用一张大的特色图像。虽然不是每个主题都需要特色图像，推荐你支持文章缩略图和特色图像。
```
add_theme_support( 'post-thumbnails' );
```

#### 文章形式
[Post formats](https://developer.wordpress.org/themes/functionality/post-formats/)允许用户以不同的形式来发布他们的文章。当博客制作者根据文章的内容来选择不同的形式和模板的时候这是很有用的。推荐的做法是在文章形式中用add_theme_support()。
```
add_theme_support( 'post-formats',  array ( 'aside', 'gallery', 'quote', 'image', 'video' ) );
```
[Learn more about post formats](https://developer.wordpress.org/themes/functionality/post-formats/)

#### 初始设置实例
包含上面那些特点就会让你的functions.php文件像下面这样。为了以后看代码清晰请添加代码注释。

如这个例子的底部所示，你必须添加必要的[add_action()](https://developer.wordpress.org/reference/functions/add_action/)声明来确保 myfirsttheme_setup 函数被加载。
```
if ( ! function_exists( 'myfirsttheme_setup' ) ) :
/**
 * Sets up theme defaults and registers support for various WordPress features.
 *
 * Note that this function is hooked into the after_setup_theme hook, which runs
 * before the init hook. The init hook is too late for some features, such as indicating
 * support post thumbnails.
 */
function myfirsttheme_setup() {

    /**
     * Make theme available for translation.
     * Translations can be placed in the /languages/ directory.
     */
    load_theme_textdomain( 'myfirsttheme', get_template_directory() . '/languages' );

    /**
     * Add default posts and comments RSS feed links to <head>.
     */
    add_theme_support( 'automatic-feed-links' );

    /**
     * Enable support for post thumbnails and featured images.
     */
    add_theme_support( 'post-thumbnails' );

    /**
     * Add support for two custom navigation menus.
     */
    register_nav_menus( array(
        'primary'   => __( 'Primary Menu', 'myfirsttheme' ),
        'secondary' => __('Secondary Menu', 'myfirsttheme' )
    ) );

    /**
     * Enable support for the following post formats:
     * aside, gallery, quote, image, and video
     */
    add_theme_support( 'post-formats', array ( 'aside', 'gallery', 'quote', 'image', 'video' ) );
}
endif; // myfirsttheme_setup
add_action( 'after_setup_theme', 'myfirsttheme_setup' );
```
#### 内容宽度
一个内容宽度是加入到你的functions.php文件中，来防止没有内容导致站点容器被破坏。内容宽度是添加到你站点中任何内容设置的最大允许宽度，包含上传的图片，在下面这个例子中，内容区域有一个800px的最大宽度，没有内容会超过这个值。
```
if ( ! isset ( $content_width) )
    $content_width = 800;
```
#### 其它
这里有些通用功能你可以引用到functions.php去，下面就是一些通用功能的清单。通过点击就可以学习更多关于这些功能的知识。
- [Custom Headers](https://developer.wordpress.org/themes/functionality/custom-headers/)
- [Sidebars](https://developer.wordpress.org/themes/functionality/sidebars/)(一些小模块)
- 自定义背景颜色(需要链接)
- 添加编辑器样式(需要链接)
- HTML5(需要链接)
- 标题标签(需要链接)

#### 你的functions.php文件
如果你选择包含上面清单上的所有的函数，你的functions.php文件也许就会像这样，上面提到的都注释了。
```
/**
 * MyFirstTheme's functions and definitions
 *
 * @package MyFirstTheme
 * @since MyFirstTheme 1.0
 */

/**
 * First, let's set the maximum content width based on the theme's design and stylesheet.
 * This will limit the width of all uploaded images and embeds.
 */
if ( ! isset( $content_width ) )
    $content_width = 800; /* pixels */

if ( ! function_exists( 'myfirsttheme_setup' ) ) :
/**
 * Sets up theme defaults and registers support for various WordPress features.
 *
 * Note that this function is hooked into the after_setup_theme hook, which runs
 * before the init hook. The init hook is too late for some features, such as indicating
 * support post thumbnails.
 */
function myfirsttheme_setup() {

    /**
     * Make theme available for translation.
     * Translations can be placed in the /languages/ directory.
     */
    load_theme_textdomain( 'myfirsttheme', get_template_directory() . '/languages' );

    /**
     * Add default posts and comments RSS feed links to <head>.
     */
    add_theme_support( 'automatic-feed-links' );

    /**
     * Enable support for post thumbnails and featured images.
     */
    add_theme_support( 'post-thumbnails' );

    /**
     * Add support for two custom navigation menus.
     */
    register_nav_menus( array(
        'primary'   => __( 'Primary Menu', 'myfirsttheme' ),
        'secondary' => __('Secondary Menu', 'myfirsttheme' )
    ) );

    /**
     * Enable support for the following post formats:
     * aside, gallery, quote, image, and video
     */
    add_theme_support( 'post-formats', array ( 'aside', 'gallery', 'quote', 'image', 'video' ) );
}
endif; // myfirsttheme_setup
add_action( 'after_setup_theme', 'myfirsttheme_setup' );
```
