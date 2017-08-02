#### Post Formats(文章形式)
一个文章形式被用于以一个确定的形式和样式来呈现文章的主题中。文章形式这个特性给所有支持此功能的主题提供标准的，可用的形式清单。也许在清单上的一个主题不能支持所有格式;在这样的情况下，最好是让用户知道这一点。

一个主题不能采用不在标准清单上的形式，甚至通过插件也不行。这个标准确保了主题和外部工具使用这个特性时的兼容性。

简而言之，在一个支持文章形式的主题中，一个博客使用者可以改变文章形式来改变文章的显示。

使用日志来举例，在过去，一个名称为Asides的分类目录被创建，这个分类目录下有些文章，然后基于样式规则从post_class()或者从in_category('asides')，来显示不同内容。

在文章形式中，有一个新的方式允许一个主题加入一个支持文章形式(
  e.g. [add_theme_support('post-formats', array('aside'))](e.g. add_theme_support('post-formats', array('aside')))
  )的功能，然后当在后台保存文章的时候，有文章形式选项可以被选择。一个名为[get_post_format($post->ID)](https://developer.wordpress.org/reference/functions/get_post_format/)可以用于决定形式，[post_class()](https://developer.wordpress.org/reference/functions/post_class/)也会创建'format-asides'纯CSS样式类。

#### 支持的形式
如果主题支持的话，下面这些文章形式会是有用的。

需要注意的是，尽管现有的文章内容不会改变，主题可以根据格式来显示不同文章，文章如何显示完全取决于主题，这里有一些不同常用的文章格式的典型用法的指导原则，
- aside(日志)-典型的没有标题的样式，类似于Facebook中的注意更新。
- gallery(相册)-一组图片附件。文章有可能包含了一组代码块和一些图片。
- link(链接)-一个链接到另一个站点。主题也许希望通过使用`<a href="">`标签在文章内容来作一个外链，另一个可选的做法，如果文章只包含一个URL，文章的标题将会是这个URL或者自己设定的文章标题。
- image(图像)-一张图片，在文章中`<img/>`标签可以被认为image类型。或者，如果文章只有一个URL，那imageURL或者文章标题的将会成为文章标题。
- quote(引语)-一个引用语，通常用blockquote来包裹引用内容。或者将引用作为文章内容，那资源/作者就成为文章标题。
- status(状态)-一个简短的状态更新，类似推特的状态更新。
- video(视频)-一个视频，`<video/>`标签或者类在文章内容中可以引入一个视频，或者，如果文章只有一个URL，那就是视频URL。如果博客想要支持这个视频形式(像通过一个插件)，可以将视频看做一个附件。
- audio(音频)-一个音频文件，可以用于播放。
- chat(聊天)-一个聊天记录，像这样子
```
1 John: foo
2 Mary: bar
3 John: foo 2
```

当在写或者编辑一个文章的时候，如果没有指定文章形式，就按标准的形式。如果指定的是一个无效的文章形式，就会默认用标准的形式。

#### 函数参考
主函数#
- [set_post_format()](https://developer.wordpress.org/reference/functions/set_post_format/)
- [get_post_format()](https://developer.wordpress.org/reference/functions/get_post_format/)
- [has_post_format()](https://developer.wordpress.org/reference/functions/has_post_format/)

其他函数#
- [get_post_format_link()](https://developer.wordpress.org/reference/functions/get_post_format_link/)
- [get_post_format_string()](https://developer.wordpress.org/reference/functions/get_post_format_string/)

#### 让主题支持
主题需要在functions.php文件中使用[add_theme_support()](https://developer.wordpress.org/reference/functions/add_theme_support/)来告诉wordpress支持哪个文章形式通过传递一个数组像这样:
```
function themename_post_formats_setup() {
    add_theme_support( 'post-formats', array( 'aside', 'gallery' ) );
}
add_action( 'after_setup_theme', 'themename_post_formats_setup' );
```
这个钩子函数[after_setup_theme](https://developer.wordpress.org/reference/hooks/after_setup_theme/)可以让主题被加载之后文章形式的功能被注册。

#### 让文章发布类型支持
发布类型需要在functions.php文件中使用[add_post_type_support()](https://developer.wordpress.org/reference/functions/add_post_type_support/)来告诉wordpress支持哪个文章形式。
```
function themename_custom_post_formats_setup() {
    // add post-formats to post_type 'page'
    add_post_type_support( 'page', 'post-formats' );

    // add post-formats to post_type 'my_custom_post_type'
    add_post_type_support( 'my_custom_post_type', 'post-formats' );
}
add_action( 'init', 'themename_custom_post_formats_setup' );
```
或者在函数[register_post_type()](https://developer.wordpress.org/reference/functions/register_post_type/)中，在supports数组参数中添加文章形式。
[add_post_type_support](https://developer.wordpress.org/reference/functions/add_post_type_support/)应该被勾住，以此来初始化hook，因为自定义发布类型也许不能通过[after_setup_theme](https://developer.wordpress.org/reference/hooks/after_setup_theme/)来注册。

#### 文章形式的使用
在主题中，使用[ get_post_format()](https://developer.wordpress.org/reference/functions/get_post_format/)来检查一个文章的形式，以及修改相应的描述。注意，默认形式下的文章会返回一个false。或者，用用[has_post_format()](https://developer.wordpress.org/reference/functions/has_post_format/)[conditional tag:](https://developer.wordpress.org/themes/basics/conditional-tags/)
```
if ( has_post_format( 'video' )) {
  echo 'this is the video format';
}
```

#### 推荐样式
还有一个形式就是通过样式规则，主题应该在包围文章的代码中使用[post_class()](https://developer.wordpress.org/reference/functions/post_class/)函数来动态添加样式类。以这种方式文章形式会引起添加额外的类，使用'format-foo'命名方式。
比如，将下面代码放入你主题的样式表中可以使状态形式的文章隐藏文章标题。
```
.format-status .post-title {
display:none;
}
```

每个形式都有对应的确定的样式，根据现代用法，最好是在应用样式的时候记住每个形式的预期用法。

比如，日志，链接，状态这些形式是简单，简短，次要的。在没有标题和作者信息的时候通常会显示这些。日志可以大概包含一到二个段落，链接可以是仅由一个链接或者一个URL组成的一个句子。链接和日志都可能在文章详情页中有一个链接(使用[the_permalink()](https://developer.wordpress.org/reference/functions/the_permalink/))并且允许有评论，但是状态形式很有可能不会有这样一个链接。

另一方面，一个典型图像文章的就是只有一张图片，没有标题/文字。音频/视频文章也是这样的除非你加上去。他们三个都可以通过插件或者标准嵌入程序[Embeds](https://codex.wordpress.org/Embeds)来显示他们的内容。标题和作者可能不会显示出来，因为内容可能是不言而喻的。

引语形式是特别适合从一个没有额外信息的人来发布一个简单引语，如果你将引语单独作为文章内容，或者将引语人物的名字放入到文章标题，然后你可以修改文章的样式来显示对应的内容[the_content](https://developer.wordpress.org/reference/functions/the_content/)除了在引语形式中重新修改样式，使用[the_title()](https://developer.wordpress.org/reference/functions/the_title/)来显示引用的人名作为署名。

一个聊天可能趋向于单行显示，在许多案例中，聊天形式带着某些样式，你可以让它显示单行字的内容。比如在一个灰色背景的div或者类似情况，这样就可以形象的区分是不是一个聊天会话了。

#### 子主题中的文章形式
[Child Themes](https://developer.wordpress.org/themes/advanced-topics/child-themes/)继承了由父主题定义的文章形式，在子主题中为了文章形式使用[add_theme_support()](https://developer.wordpress.org/reference/functions/add_theme_support/)的优先级必须是落后与父主题，这样将会推翻已有的列表，不加入到它
```
add_action( 'after_setup_theme', 'childtheme_formats', 11 );
function childtheme_formats(){
     add_theme_support( 'post-formats', array( 'aside', 'gallery', 'link' ) );
}
```
使用[remove_theme_support('post-formats') ](https://developer.wordpress.org/reference/functions/remove_theme_support/)将会移除所有。
