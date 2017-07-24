## 循环（the loop）
**循环**是WordPress用来通过主题模板文件输出文章的默认机制,检索多少篇文章取决于在阅读设置中定义的每个页面的数量。在这个循环中，wordpress检索每一个文章，在当前页面上显示，并根据您的主题的说明对它进行格式化。

**循环**会为每一篇文章从wordpress数据库中提取数据，并且在每个模板标签中插入相关信息。在循环中，每篇文章中的html和php代码都会得到处理。

简单来讲，循环是名符其实的：在某一时间，它为当前页面循环遍历每篇文章，并执行你主题的指定动作。

你可以用循环来做不同的事情，比如：
- ** ** 显示文章标题和设置你的博客的主页。
- ** ** 在文章详情页中显示内容和评论。
- ** ** 为一个正在使用模板标签的页面显示内容。
- ** ** 从自定义发布类型POST TYPES和自定义字段FIELd中显示内容。
你可以通过模板文件自定义循环，来显示和操作不同的内容。
#### 循环详细说明 #
最基本最简单的循环：
~~~
<?php if ( have_posts() ) : ?>
    <?php while ( have_posts() ) : the_post(); ?>
        ... Display post content
    <?php endwhile; ?>
<?php endif; ?>
~~~
这个循环的意思是，当如果有文章时，循环开始并且显示文章。
说的更细点就是：
- ** **这个have_posts()函数会检查是否存在文章。
- ** **如果存在文章，一个while循环将会开始，并且while循环的判断条件中如果它是真的，只要have_posts()继续存在文章，循环就会继续。
#### 使用循环
循环应该被放置在index.php中，或者是任何被用于显示文章信息的模板中。因为你不想重复你的header一遍又一遍，所以循环应该被放置在get_header()之后。比如：
~~~
<?php get_header(); ?>
<?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
    ... Display post content
<?php endwhile; endif; ?>
~~~
在上面的例子中，循环的末尾声明了endwhile和endif,循环必须以if声明和while声明开始，同上，结尾必须以这样的方式来结尾。

任何你希望应用到所有文章的模板标签必须存在于开始声明和结束声明之间。

>如果找不到指定条件文章，你可以引用一个自定义的404,notfound信息来显示。如下面的例子所示，这个信息必须放在endwhile声明和endif声明之间。

一个简单的index.php看起来应该像这样:
```
<?php
    get_header();
    if ( have_posts() ) : while ( have_posts() ) : the_post();
        the_content();
    endwhile;
    else :
        _e( 'Sorry, no posts matched your criteria.', 'textdomain' );
    endif;
    get_sidebar();
    get_footer();
?>
```
#### 循环可以显示什么？
循环可以为每篇文章显示许多不同的元素。举例来说，一些常用标签可以用于不同的主题像下面这些：
- [next_post_link()](https://developer.wordpress.org/reference/functions/next_post_link/)-一个可以链接到当前文章的下一篇文章的链接，文章按发布时间排序。

- [previouys_post_link()](https://developer.wordpress.org/reference/functions/previous_post_link/)-一个可以链接到当前文章的上一篇文章的链接，文章按发布时间排序。

- [the_category()](https://developer.wordpress.org/reference/functions/the_category/)-正在被查看的文章或者页面的分类或者关联分类。

- [the_author()](https://developer.wordpress.org/reference/functions/the_author/)-文章或者页面的作者。

- [the_content()](https://developer.wordpress.org/reference/functions/the_content/)-文章或者页面的主要内容。

- [the_excerpt()](https://developer.wordpress.org/reference/functions/the_excerpt/)-文章的摘要，一篇文章的前55个单词后面跟着省略号（...）,或者读取更多这个链接，链接到完整的文章。你也可以使用文章的‘Excerpt’功能来自定义一个特定长度的摘要。

- [the_ID()](https://developer.wordpress.org/reference/functions/the_id/)-文章或者页面的ID。

- [the_meta()](https://developer.wordpress.org/reference/functions/the_meta/)-文章或者页面相关联的自定义字段。

- [the_shortlink()](https://developer.wordpress.org/reference/functions/the_shortlink/)-一个通过url或者ID链接到当前网页的页面或者文章的链接。

- [the_tags()](https://developer.wordpress.org/reference/functions/the_tags/)-文章的标签或者与之相关的标签。

- [the_title()](https://developer.wordpress.org/reference/functions/the_title/)-文章或者页面的标题。

- [the_time()](https://developer.wordpress.org/reference/functions/the_time/)-文章或页面的时间或者日期，这个可以在标准php日期函数格式化的时候自定义。

你也可以使用 [条件标签](https://developer.wordpress.org/themes/basics/conditional-tags/)，如：
- [is_home()](https://developer.wordpress.org/reference/functions/is_home/)-当当前页面为主页的时候返回true。

- [is_admin()](https://developer.wordpress.org/reference/functions/is_admin/)-当在管理员界面的时候返回true,否则为false。

- [is_single()](https://developer.wordpress.org/reference/functions/is_single/)-当当前页面为文章详情页的时候返回true。

- [is_page()](https://developer.wordpress.org/reference/functions/is_page/)-当当前页面为page的时候返回true。

- [is_page_template()](https://developer.wordpress.org/reference/functions/is_page_template/)-可以用来判断一个页面是否使用了特定的模板，比如：is_page_template('about-page.php')。

- [is_category()](https://developer.wordpress.org/reference/functions/is_category/)-当文章或者页面拥有指定的分类目录，就返回true，比如:is_category('news')。

- [is_tag()](https://developer.wordpress.org/reference/functions/is_tag/)-当文章或者页面拥有指定的标签，就返回true。

- [is_author()](https://developer.wordpress.org/reference/functions/is_author/)-当当前在作者的归档页面就返回true。

- [is_search()](https://developer.wordpress.org/reference/functions/is_search/)-当前页面为搜索结果页时返回true。

- [is_404()](https://developer.wordpress.org/reference/functions/is_404/)-当前页面不存在返回true。

- [has_excerpt()](https://developer.wordpress.org/reference/functions/has_excerpt/)-当前文章或页面有摘要的时候就返回true。

#### 实例
一起来看看循环在实际使用中的一些例子
#### 简单例子
##### 博客归档页 Blog Archive
很多博客有一个博客归档页，可以显示很多信息，如文章的title(标题),thumbnail(缩略图),excerpt(摘要)。下面的例子演示了一个简单的循环，这个循环用于检查是否有任何文章，如果有，输出每个文章的title,thumbnail,excerpt。如果不存在，则显示自定义的信息。
```
<?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>

        <h2><?php the_title(); ?></h2>
    <?php the_post_thumbnail(); ?>
    <?php the_excerpt(); ?>
<?php endwhile; else: ?>
    <?php _e( 'Sorry, no posts matched your criteria.', 'textdomain' ); ?>
<?php endif; ?>
```
#### 单个文章 Individual Post

在wordpress中，每个文章都有自己的页面，用于显示对应的文章的信息，模板文件允许你自定义你想显示的信息。
在以下的实例中，循环输出了文章的标题和内容。你可以通过这个例子在文章或者页面模板文件中来显示页面大部分的基本信息。你也可以自定义这个模板来给文章添加更多的数据，比如这个category的例子。
```
<?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>

<h1><?php the_title(); ?></h1>
    <?php the_content(); ?>
<?php endwhile; else: ?>
    <?php _e( 'Sorry, no pages matched your criteria.', 'textdomain' ); ?>
<?php endif; ?>
```
#### 稍微难点的例子
##### 从不同的分类目录中定义文章
以下的例子做了这些事：
- 第一，显示每篇文章对应的标题，时间，作者，内容，分类，类似于单个文章的案例
- 下一步，为了让categoryID为3下的文章定义不同的样式，使用in_category()模板标签。
在此例子中，在每个循环部分都提供了详细的代码注释。

```
// Start the Loop.
<?php if ( have_posts() ) : while ( have_posts() ) : the_post();
/* * See if the current post is in category 3.
   * If it is, the div is given the CSS class "post-category-three".
   * Otherwise, the div is given the CSS class "post".
*/
if ( in_category( 3 ) ) : ?>
<div class="post-category-three">
    <?php else : ?>
<div class="post">
    <?php endif; ?>
        // Display the post's title.
        <h2><?php the_title() ?></h2>
        // Display a link to other posts by this posts author.
        <small><?php _e( 'Posted by ', 'textdomain' ); the_author_posts_link() ?></small>
        // Display the post's content in a div.
        <div class="entry">
            <?php the_content() ?>
        </div>
        // Display a comma separated list of the post's categories.
        <?php _e( 'Posted in ', 'textdomain' ); the_category( ', ' ); ?>
    // closes the first div box with the class of "post" or "post-cat-three"
    </div>
// Stop the Loop, but allow for a "if not posts" situation
<?php endwhile; else :
/*
 * The very first "if" tested to see if there were any posts to
 * display. This "else" part tells what do if there weren't any.
 */
_e( 'Sorry, no posts matched your criteria.', 'textdomain' );
 // Completely stop the Loop.
 endif;
?>
```
#### 移除这个部分
>这个部分应该被移除，但是它存在的原因是因为在插件手册中有个在主题框中无法正确显示下一部分的bug。

#### 多重循环
在某些情况下，你或许需要使用到更多的单循环。例如，你也许会想在页面的顶部以一个表格的形式在内容列表中显示文章的标题，并且在页面下部显示内容。因为查询没有被更改，我们仅仅只需要在第二次循环的时候返回循环。因此，我们会用到这个函数
[rewind_posts()](https://developer.wordpress.org/reference/functions/rewind_posts/)。

#### rewind_posts的用法
你可以使用rewind_posts()来对同一个查询来循环遍历两次，这点在当你想在同一个页面不同地方显示同一个查询两次的时候是很有用的。

这里是一个rewind_posts的使用实例:
```
// Start the main loop
<?php
    if ( have_posts() ) : while ( have_posts() ) : the_post();
        the_title();
    endwhile;
    endif;

    // Use rewind_posts() to use the query a second time.
    rewind_posts();

    // Start a new loop
    while ( have_posts() ) : the_post();
        the_content();
    endwhile;
?>
```

#### 创建次要的查询与循环
通过同一个查询来循环两次的做法相对简单，但是你会不仅仅使用到它。相反的，你会经常想创建一个次要的查询来在模板中显示不同的内容。例如，你也许想在同一个页面中显示两组分类下的文章，除了每组做不同的事。这里有一个通用的例子，如下所示，在下面的文章页中，通过次要循环我们可以在一个文章页中显示两种不同分类目录下的文章。
```
<?php
    // The main query.
    if ( have_posts() ) : while ( have_posts() ) : the_post();
        the_title();                                                             
        the_content();                                                          
    endwhile;                                                                   
    else :                                                                      
        // When no posts are found, output this text.                           
        _e( 'Sorry, no posts matched your criteria.' );                         
    endif;                                                                       
    wp_reset_postdata();                                                        

    /*                                                                          
     * The secondary query. Note that you can use any category name here. In our example,
     * we use "example-category".                                               
     */                                                                        
    $secondary_query = new WP_Query( 'category_name=example-category' );        

    // The second loop. if ( $secondary_query->have_posts() )
    echo '<ul>';
    while ( $secondary_query->have_posts() ) :
        $secondary_query->the_post();
        echo '<li>' . get_the_title() . '</li>';
    endwhile;
    echo '</ul>';
    endif;
wp_reset_postdata();
?>
```
如你所见，在上面的例子中，我们首先进行了一个常规循环，然后我们又定义了一个新的变量使用[wp_query](https://developer.wordpress.org/reference/classes/wp_query/)这个来查询了一个指定的分类目录，在我们的例子中我们选择了category-slug.php别名的形式来进行查询。

上面的常规循环有点需要注意，它通过[wp_reset_postdata()](https://developer.wordpress.org/reference/functions/wp_reset_postdata/)来重置了文章查询数据。在你使用第二次循环之前，你必须要重置文章查询数据，这里还有两种方式来实现:
1:通过使用[rewind_posts()](https://developer.wordpress.org/reference/functions/rewind_posts/)函数，或者
2.创建新的query(查询)类。

多重循环的重置

重置那些你正在使用到模板当中的多重循环是很重要的，是否不这样做将会导致不可预料的结果取决于在全局变量$post下数据是如何被使用与存储的。这里依赖了三种重置循环的主要方式，它们是：
- [wp_reset_postdata()](https://developer.wordpress.org/reference/functions/wp_reset_postdata/)
- [wp_reset_query()](https://developer.wordpress.org/reference/functions/wp_reset_query/)
- [rewind_posts()](https://developer.wordpress.org/reference/functions/rewind_posts/)

#### [wp_reset_postdata()](https://developer.wordpress.org/reference/functions/wp_reset_postdata/)的用法
当你在通过WP_Query进行自定义或者多重循环的时候使用[wp_reset_postdata()](https://developer.wordpress.org/reference/functions/wp_reset_postdata/)。在当前的文章页面的主查询中，这个函数重置了全局变量$post。如果你遵循最佳实践，那么在你重置循环的过程中这个是最常用的函数。

为了正确的使用这个函数，将下面的代码放置在任何WP_Query的循环之后。
```
<?php wp_reset_postdata(); ?>
```
这里是一个通过[wp_reset_postdata()](https://developer.wordpress.org/reference/functions/wp_reset_postdata/)函数来重置WP_Query查询的例子。
```
<?php
// Example argument that defines three posts per page.
$args = array( 'posts_per_page' => 3 );

// Variable to call WP_Query.
$the_query = new WP_Query( $args );

if ( $the_query->have_posts() ) :
    // Start the Loop
    while ( $the_query->have_posts() ) : $the_query->the_post();
        the_title();
        the_excerpt();
    // End the Loop
    endwhile;
else:
    // If no posts match this query, output this text.
    _e( 'Sorry, no posts matched your criteria.', 'textdomain' );
endif;
wp_reset_postdata();

?>
```
[wp_reset_query()](https://developer.wordpress.org/reference/functions/wp_reset_query/)的用法

使用[wp_reset_query()](https://developer.wordpress.org/reference/functions/wp_reset_query/)将WP_Query查询类和全局变量$post的数据恢复到最初始的主查询。如果你在你的循环里使用的是[query_posts()](https://developer.wordpress.org/reference/functions/query_posts/)那么你必须使用这个函数来重置你的循环.
你可以在[WP_Query](https://developer.wordpress.org/reference/classes/wp_query/)的自定义循环之后使用它，因为它在运行的时候实际上调用的是[wp_reset_postdata()](https://developer.wordpress.org/reference/functions/wp_reset_postdata/)。无论如何，在任何使用WP_Query来自定义查询当中使用[wp_reset_postdata()](https://developer.wordpress.org/reference/functions/wp_reset_postdata/)是最佳实践。

> [query_posts()](https://developer.wordpress.org/reference/functions/query_posts/)这个函数不是最佳实践，而且是尽可能要避免的。因此，你不应该用太多[wp_reset_query()](https://developer.wordpress.org/reference/functions/wp_reset_query/).

为了正确使用这个函数，将下面的代码放置在任何通过[query_posts()](https://developer.wordpress.org/reference/functions/query_posts/)进行的查询之后。

```
<?php wp_reset_query(); ?>
```
