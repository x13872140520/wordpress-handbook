#### 模板标签
模板标签被用在主题从数据库中提取内容。内容可能是任何东西，从一个博客标题到一个完整的侧边栏。模板标签是往你主题添加内容的好办法，因为:
- 它们可以动态输出内容
- 可以在多个模板文件中使用它们
- 它们将主题拆分成更小，更容易理解的节段。

#### 什么是一个模板标签
一个模板标签是一个简单的一小段代码，来告诉wordpress从数据库中取出哪些东西。可以分为三大类:
- 一个PHP代码标签
- 一个wordpress函数
- 可选的参数

你可以通过一个模板标签从数据库中引用另一个主题文件或者一些信息。

比如，这个[get_header()](https://developer.wordpress.org/reference/functions/get_header/)模板标签告诉wordpres获取header.php文件并在当前主题文件中使用它。类似的，[get_footer()](https://developer.wordpress.org/reference/functions/get_footer/)告诉wordpress来获得footer.php文件。

这里还有一些其他的模板标签:
- [the_title()](https://developer.wordpress.org/reference/functions/the_title/) -告诉wordpress从数据库中获得页面或者文章的标题并使用它。
- [bloginfo( 'name' )](https://developer.wordpress.org/reference/functions/bloginfo/) -告诉wordpress从数据库中获取博客标题并将其包含在模板文件中。

如果你仔细看了最后一个例子，你会发现那有个参数在()内。参数让你做了两件事:
-   1.访问指定的信息
-   2.以一个确定的方式格式化信息
[Parameters are covered extensively below](https://developer.wordpress.org/themes/basics/template-tags/#parameters)(这里详细介绍了参数),你可发送wordpress指定指令来说明你想数据怎样来显示。

#### 为什么使用模板标签
通过将特定的一块内容的全部代码封装起来，模板标签可以很容易的将模板文件的各种部分包含到一个主题文件中，在维护主题的时候也这样。

在一个主题文件中要引用主题模板文件,像single.php,page.php,front-page.php等等。通过创建一个header.php文件，再用[get_header()](https://developer.wordpress.org/reference/functions/get_header/)比复制，粘贴到模板文件要容易得多。也让以后的维护变得更容易。不论何时你在你的header.php文件中作了修改，修改的内容会自动覆盖到你所有用到get_header的主题文件。

另外一个使用模板标签的原因是动态展示数据，从数据库中i.e数据，在你的头部，你可以像这样手动包含标题标签:
```
<title>My Personal Website<title>
```
无论如何，当你想在任何你想改变你站点标题的时候，就意味着你要手动编辑你的主题。相反，使用[bloginfo('name')](https://developer.wordpress.org/reference/functions/bloginfo/)模板标签就可以让其变得更容易，它会自动修改数据中站点的标题。现在，你可以在wordpress中修改你网页的标题，而不是在主题模板中硬生生的写代码。

#### 怎样使用模板标签
使用模板标签是非常简单的，在任何模板文件中你可以通过输出一行简单的php代码来引用模板标签。输出header.php文件就像下面这样简单:
```
get_header()
```

#### 参数
一些模板标签需要你通过参数，参数是决定从数据库中取出什么的额外信息。

比如，[bloginfo()](https://developer.wordpress.org/reference/functions/bloginfo/)模板标签允许你往里面传一个参数来告诉wordpress你想找的特定的信息。为了输出博客名字.你只需要通过'name'和这个参数,像这样:
```
bloginfo('name');
```
为了输出wordpress运行的blog版本，你可以输入一个'version'参数:
```
bloginfo('version');
```
因为每个模板标签的参数是不同的，这里有一个清单关于那些特定的模板标签的参数以及它们能做什么，通过[code reference](https://developer.wordpress.org/reference/).

#### 在循环下的模板标签的用法
许多模板标签工作在wordpress循环下，这就意味在模板文件中的PHP循环体中包含他们，通常网页用户所看到的是基于循环内部的指令。

wordpress循环像这样开始:
```
if ( have_posts() ) :
    while ( have_posts() ) :
        the_post();
```
那些工作在循环内的模板标签必须在中间部分，在循环结束之前，像下面这样:
```
endwhile;
else :
    _e( 'Sorry, no posts matched your criteria.', 'devhub' );
endif;
```

这些模板标签需要放在循环的里面来用:
- [the_content()](https://developer.wordpress.org/reference/functions/the_content/)
- [the_excerpt()](https://developer.wordpress.org/reference/functions/the_excerpt/)
- [next_post()](https://developer.wordpress.org/reference/functions/next_post/)
- [previous_post()](https://developer.wordpress.org/reference/functions/previous_post/)

为什么有些函数需要循环是因为他们需要全局post类将被设置。

如果你想使用不需要在循环下的模板标签。
- [wp_list_cats()](https://developer.wordpress.org/reference/functions/wp_list_cats/)
- [wp_list_pages()](https://developer.wordpress.org/reference/functions/wp_list_pages/)

然后你可以将它放入任何你想放入的文件，例如，在sidebar,header,footer模板文件中。

这些是典型不需要全局post类的函数。

#### 参阅
- [Conditional Tags](https://developer.wordpress.org/themes/basics/conditional-tags/)
- [Complete list of Template Tags](https://developer.wordpress.org/themes/references/list-of-template-tags/)
