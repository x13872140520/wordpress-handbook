#### 主题文件的组织结构 Organizing Theme Files
在技术上来讲，wordpress主题仅仅需要两个文件(index.php和style.css)，他们通常由很多个文件组成。那就意味着他们很快就会变得杂乱无章，这个部分将会演示如何组织你的文件结构。

> 从wordpress3.0以来，没有什么有用的方法来代替主题中如果没有header.php和footer.php的情况。你的主题或许需要包含这些文件。

#### 主题文件夹和文件的层次结构
如先前提到的，默认的Twenty themes是好的主题开发的最好的例子。例如，这里演示了[Twenty Seventeen Theme](https://wordpress.org/themes/twentyseventeen/)如何组织它的[file structure](https://core.trac.wordpress.org/browser/trunk/src/wp-content/themes/twentyseventeen).
```
assets (dir)
      - css (dir)
      - images (dir)
      - js (dir)
inc (dir)
template-parts (dir)
      - footer (dir)
      - header (dir)
      - navigation (dir)
      - page (dir)
      - post (dir)
404.php
archive.php
comments.php
footer.php
front-page.php
functions.php
header.php
index.php
page.php
README.txt
rtl.css
screenshot.png
search.php
searchform.php
sidebar.php
single.php
style.css
```
你可以看到那些在根目录下的主要的主题模板文件，JavaScript, CSS, images全部被放置在assets文件夹，template-parts被放置在各自的子文件夹下，与核心功能有关的函数集合被放置在inc文件夹下。

说到这里，在wordpress主题下这些都是非必要文件夹。无论如何，wordpress会默认的组织下面这些文件夹。

>style.css 应该放在在你的主题根目录下，而不是在CSS文件夹里

语言文件夹

最佳实践就是[internationalize your theme](https://developer.wordpress.org/themes/functionality/internationalization/)(国际化你的主题)让它可以被翻译成其他的语言。默认主题包含了languages文件夹，其中包含了*.pot翻译文件和*.mo全翻译文件。
languages是文件夹的默认名字，你可以改变它的名字。如果你这样做，你必须更新[load_theme_textdomain()](https://developer.wordpress.org/reference/functions/load_theme_textdomain/)
