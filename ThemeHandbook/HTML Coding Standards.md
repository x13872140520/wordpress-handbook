#### HTML编码标准
HTML
validation(验证)
所有html页面都应该通过[ the W3C validator](http://validator.w3.org/)来确保标记的格式良好，这本身并不能象征是好的代码。但是它帮助清除问题，通过自动化测试。这样并不能省略手动审查代码。(对于其他验证器，参见[ HTML Validation](https://codex.wordpress.org/Validating_a_Website#HTML_-_Validation)).

#### 自闭合元素
所有标签都应该正确闭合，像包围text或其他元素的节点的标签，终端是一个微不足道的任务。对于自闭和标签，斜杠前应该有一个确定的空格:
```
<br />
```
比这种不规范的方式要好:
```
<br/>
```
w3c规定了自闭和标签斜杠前应该有空格，参见[source](http://www.w3.org/TR/xhtml1/#C_2)

#### 属性和标签
所有的标签和属性必须用小写,此外，当文本的目的是为了让机器解释的收属性值应该小写。相反如果数据需要给人阅读，需要像下面这样用大写。

机器看的:
```
<meta http-equiv="content-type" content="text/html; charset=utf-8" />
```
人看的:
```
<a href="http://example.com/" title="Description Here">Example.com</a>

```

#### 引号
根据XHTML的W3C规范，所有属性必须有值，而且必须使用单引号或者双引号。下面的是属性/值对的引号的恰当的和不恰当的用法。

正确的:
```
<input type="text" name="email" disabled="disabled" />
<input type='text' name='email' disabled='disabled' />
```
不正确的:
```
<input type=text name=email disabled>
```
在HTML中，不是所有的属性都必须有值，属性值也不是一直都要有引号。尽管上面所有的例子都是有效的HTML,不给属性用引号可能会导致安全缺陷。所以永远都要给属性引号。

#### 缩进
与PHP一样，HTML的缩进应该一直反应逻辑结构。使用tab而不是空格。

当PHP与HTML混合在一起的时候，缩进PHP代码以匹配周围的HTML。闭合PHP应该与开头的PHP有相同的缩进。

正确:
```
<?php if ( ! have_posts() ) : ?>
    <div id="post-1" class="post">
        <h1 class="entry-title">Not Found</h1>
        <div class="entry-content">
            <p>Apologies, but no results were found.</p>
            <?php get_search_form(); ?>
        </div>
    </div>
<?php endif; ?>
```
不正确:
```
        <?php if ( ! have_posts() ) : ?>
        <div id="post-0" class="post error404 not-found">
            <h1 class="entry-title">Not Found</h1>
            <div class="entry-content">
            <p>Apologies, but no results were found.</p>
<?php get_search_form(); ?>
            </div>
        </div>
<?php endif; ?>

```

#### 鸣谢
- HTML编码标准改编自[Fellowship Tech Code Standards (CC license)](http://developer.fellowshipone.com/patterns/code.php)
