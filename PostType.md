#### 发布类型PostType
在wordpress中发布任何内容的时候都会区分很多不同的类型，这些内容的类型的概念我们通常称之为发布类型(PostType),这点可能会让人有点困惑，因为它在wordpress的指的是所有不同的内容类型。例如，一个文章(post)是一个指定的发布类型(PostType),一个页面(page)也是。

所有的发布类型被存储在统一个地方-在名为wp_posts的数据库表中-用一个名为post_type的数据库列来区分。

除了默认的发布类型之外，你还可以创建自定义的发布类型。

在[Template files](https://developer.wordpress.org/themes/basics/template-files/)这个网页中简单的提到不同的模板文件会显示不同的发布类型。一个模板文件的最终目的就是用一种确定的方式来显示内容，发布类型的作用是用来对你所处理的内容进行分类。通常来说，一个模板文件对应了一个发布类型。


默认发布类型

这里有5中默认的发布类型可供于用户或者wordpress内部使用:
- Post (Post Type: ‘post’)
- Page (Post Type: ‘page’)
- Attachment (Post Type: ‘attachment’)
- Revision (Post Type: ‘revision’)
- Navigation menu (Post Type: ‘nav_menu_item’)

以上的发布类型可以通过一个插件或者主题来修改和移除，但是不推荐你移除那些成熟的主题或插件中的自带的。

作为一个主题开发者你所接触到最常用的发布类型是Post(文章), Page(页面), Attachment(附件), and Custom Post Types(自定义发布类型)。
在手册这里补充Revision类型和Navigation Menu类型已经超出本文所讲的范围。但是，重要的是你要在手册后面注意到有更多关于使用[navigation menus](https://developer.wordpress.org/themes/functionality/navigation-menus/)细节。

#### 文章(Post)

文章用于博客中，他们：
- 按时间发布顺序排序，最新的文章排最前。
- 有时间和日期标记
- 可以有默认的分类目录和标签选项
- 被用来创建feeds

那些显示了文章发布类型的模板文件:
- single.php and single-post.php
- category.php 和所有后代，如category-xxx.php
- tag.php 和所有后代
- taxonomy.php 和所有后代
- archive.php 和所有后代
- author.php 和所有后代
- date.php 和所有后代
- search.php
- home.php
- index.php

另外，主题开发人员可以在front-page.php中显示文章发布类型，如果他们愿意的话。

[Read more about Post Template Files](https://developer.wordpress.org/themes/template-files-section/post-template-files/).

#### 页面(page)
页面是一个静态发布类型，超出了正常博客的需求(一般博客页面不会用到这个类型)。他们的特点是:
- 没有时间依赖和没有时间标记
- 在编辑页面的时候不能被分类目录和/或标签来进行分类组织
- 他们可以有模板选项
- 在编辑的时候有层次结构-页面可以被设置为其他页面的父/子级

那些显示了页面发布类型的模板文件有:
- page.php 和所有后代
- $custom.php 和所有后代
- front-page.php
- search.php
- index.php

[Read more about Page Template Files](https://developer.wordpress.org/themes/template-files-section/page-template-files/).

#### 附件(Attachment)
附件常常用于在内容中显示图片或者多媒体，还可以用于连接到有关系的文件，他们的特点是：
- 通过多媒体上传系统确定那些上传文件的信息（比如名字或者描述）
- 针对图片，它包含了存储在wp_postmeta数据表中的元数据信息(包含了尺寸，缩略图，路径，等等)

那些显示了附件发布类型的模板文件有:
- MIME_type.php
- attachment.php
- single-attachment.php
- single.php
- index.php

[Read more about Attachment Template Files](https://developer.wordpress.org/themes/template-files-section/attachment-template-files/).

#### 自定义发布类型
在使用自定义发布类型的时候，你可以创建你自己的发布类型。不推荐你在你的主题中放置这种功能，这类型的功能应该被放置在一个插件中。这样就保证了你用户的内容的可移植性，如果主题被更改，存储在自定义发布类型中的内容将不会消失。

你可以通过[creating custom post types in the WordPress Plugin Developer Handbook](https://developer.wordpress.org/plugins/post-types/registering-custom-post-types/)学习更多。

通常情况下你不会在你的主题中开发自定义发布类型，你或许想要编写一些方法来显示由插件所创建的自定义发布类型。下面这些模板可以显示自定义发布类型:
- single-{post-type}.php
- archive-{post-type}.php
- search.php
- index.php

另外，通常在使用多重循环([multiple loops](https://developer.wordpress.org/themes/basics/the-loop/#multiple-loops))的时候，主题开发人员可以在任何模板文件中显示自定义发布类型。
