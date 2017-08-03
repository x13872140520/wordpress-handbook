#### 术语表
这个文档用来解释用户可能不熟悉的，wordpress独有的各种专业术语。
如果你是一名贡献者，请不要为已有的术语(如api,php,javascript等等)重新定义。

### 绝对路径（Absolute Path）

```绝对路径``` 或```完整路径```，均为文件或者目录名称在计算机或文件系统所处的独特位置的描述方式。绝对路径一般以根目录的位置或驱动盘符号作为开头，用斜线（/）的格式来分割统一路径下的目录和子目录。

```
例如：/Users/Matt/www/blog/images/icecream.jpg
```
找到一个页面的绝对路径，可以将以下文字复制到一个新的文本文件，并保存为path.php（这样可以制作一个简单的PHP网页）并上传到你的服务器上，然后使用浏览器打开该文件的URL地址(例如：http://www.example.com/path.php)。
```
<?php
 $p = getcwd();
 echo $p;
 ?>
```
- 参考资料：相对路径
- 外部链接：Path (computing) at Wikipedia

### 绝对 URI（Absolute URI）
即完整的URL.
```
http://www.example.com/blog/images/icecream.jpg
 ftp://ftp.example.com/users/h/harriet/www/
```

### Apache
Apache 是 [Apache HTTP Server Project（Apache 超文本传输协议服务器项目）](http://httpd.apache.org/) 的缩写。它是个功能强大、免费但可与商业软件媲美的[网页服务器](https://codex.wordpress.org/zh-cn:%E6%9C%AF%E8%AF%AD%E8%A1%A8#Web_server)。它由 [Apache 软件基金会开发](http://www.apache.org/)。它是互联网上最流行的网页服务器软件，拥有很多平台上的版本，如 Windows、[Unix](#Unix)/[Linux](#Linux) 和 Mac OS X。Apache 是您搭建 WordPress 站点需要的重要基础。

### 数组（Array）
数组是计算机编程的基础数据结构之一。一段数组包含了一串实体，如一串数字或字符。程序员可以通过数组的方式随机的存取一段数据。这段数据可以被存为一维数组或者多维数组。

一段一维数组的七个要素包含：

<table>
<tr>
  <td>105</td>
  <td>200</td>
  <td>54</td>
  <td>53</td>
  <td>102</td>
  <td>13</td>
  <td>405</td>
</tr>
</table>

[模板](https://codex.wordpress.org/Template_Tags) [wp_list_categories()](https://developer.wordpress.org/reference/functions/wp_list_categories/)使用的一个一维数组来显示以上参数。

一个7乘3大小的2维数组，可以表示为：
<table>
<tr>
  <td>105</td>
  <td>200</td>
  <td>54</td>
  <td>53</td>
  <td>102</td>
  <td>13</td>
  <td>405</td>
</tr>
<tr>
  <td>15</td>
  <td>210</td>
  <td>14</td>
  <td>513</td>
  <td>2</td>
  <td>2313</td>
  <td>4512</td>
</tr>
<tr>
  <td>501</td>
  <td>500</td>
  <td>499</td>
  <td>488</td>
  <td>552</td>
  <td>75</td>
  <td>1952</td>
</tr>
</table>

- 外部链接:[Array Programming at Wikipedia](https://en.wikipedia.org/wiki/Array_programming),[Array at freedictionary.com](http://encyclopedia.thefreedictionary.com/array)

### ASCII
ASCII（发音为“ask ee”）是American Standard Code for Information Interchange（美国信息交换标准代码）的缩写。它是一套用来表示数字、字母、标点符号和其它符号的标准代码。

- 外部链接:[维基百科ASCII](http://zh.wikipedia.org/wiki/ASCII)

### Atom
一种类似新闻类的网页方式来整合内容，通过news readers或者aggregators的Atom-aware程序来查看。
- 参见:[news reader](#news),[RSS](#rss),[RDF](#rdf)
- 外部链接:[Atom (standard) at Wikipedia](https://en.wikipedia.org/wiki/Atom_(standard))

### 头像（Avatar）
代表用户的图片或者图形肖像。
- 参见[gravatar](#gravatar)
- 相关文章[Using Gravatars](https://codex.wordpress.org/Using_Gravatars)
- 外部链接:[Avatar (computing) at Wikipedia](https://en.wikipedia.org/wiki/Avatar_%28computing%29)

### 二进制文件（Binaries）
二进制文件指的是编译后的计算机程序或可执行文件。许多[开源项目](https://en.wikipedia.org/wiki/Open-source_model)，可以从[源代码](https://en.wikipedia.org/wiki/Source_code)重新编译，给多数流行的平台和开源系统提供预编译的二进制文件。

### 博客（Blog）
博客，或网志，是在线日志、日记，或是连载之类的内容。它可以由一个人撰写，也可能由一群人共同编写。

一个博客通常由一个人或者一些同龄人来维护，有时公司和组织也会拥有博客。在众多企业中，目前通常是一些设计作坊、网络媒体公司，或一些尖端的科技企业。

人们不仅在博客中记录公开内容，有时也会写下私密内容。这取决于他们所使用的[内容管理系统](#ContentManagementSystem)，有些作者还有可能通过账户或密码来限制某些特别私密的博客文章的访问。

### 写博客（Blogging）
blogging是一种写博客的行为。写博客就是在博客里写点东西。这有时涉及[连接](https://en.wikipedia.org/wiki/Hyperlink)到作者在互联网上发现的一些有趣的东西。

### 博客圈（Blogosphere）
博客圈是互联网网站的一个自己，或者是与博客相关的，
- 参见[Blog](#Blog),[Blogroll](#Blogroll)

### 链接表（Blogroll）
链接表是一个由多个博客或者新站点的链接组成的清单，通常链接表被一个跟踪表上的每个站点的更新的服务所遍历，并且在一个表单形式的清单中提供所有的更新信息。
- 参见[Blog](#Blog)，[blogosphere](#blogosphere),[ feed](# feed),[news reader](#news-reader)
- 外部链接:[News aggregator at Wikipedia](https://en.wikipedia.org/wiki/News_aggregator)

### Bookmarklet 小书签（Bookmarklet）
Bookmarklet是包含了脚本代码，通常写在javascript里，允许用户执行某个函数。

例子
- wordpress的bookmarklet允许用户快速的转发他们当前所浏览的网页。
- [delicious.com bookmarklets](http://delicious.com/help/bookmarklets)允许一个用户快速的发布一个链接到他的delicious.com bookmarklets清单中。
- [Tantek's favelets](http://tantek.com/favelets/)

### 布尔型变量（Boolean）
一种值不是true就是false的变量或者表达式。
- 外部链接:[PHP Boolean data type](http://us2.php.net/manual/en/language.types.boolean.php)

### 分类目录（Category）
在wordpress下的每篇文章是category下的一个文件，分类法允许文章被跟其他类似于一个网页的导航的内容组织在一起。请注意，文章分类不应该与在用于分类和链接管理[Link Categories](#Link-Categories)的链接分类混淆在一起。

### 用户权限（Capabilities）
与用户身份验证和访问控制相关的条款，它是RBAC的权限的一个采用。在wordpress中大约有30个用户权限，看[Roles and Capabilities](https://codex.wordpress.org/Roles_and_Capabilities)概念的描述和[权限列表](https://codex.wordpress.org/Roles_and_Capabilities)

### 通用网关接口（CGI）
CGI (Common Gateway Interface)是一种指定的服务器端[server-side](https://en.wikipedia.org/wiki/Server-side)通信脚本，被设计用来在web服务器与web客户端之间传输信息。典型的，一旦用户提交之后，通过表单搜集数据的HTML页面使用了CGI程序来处理表单数据。

### 字符实体（Character Entity）
字符实体是一种用来显示特殊字符的方法，通常在HTML中使用。
比如，<和>被当做HTML标签结构的一部分来使用，所以这两个符号是被保留的。但是，如果你需要在你的站点中显示那些符号，你可以使用字符实体。比如:
对<符号使用&lt;
对>符号使用&gt;  
- 相关文章:[Fun Character Entities](https://codex.wordpress.org/Fun_Character_Entities)

### 字符集（Character Set）
一个字符集（Character Set）是这些符号(字母，数字，标点符号，特殊字符)的集合，当一起使用的时候，用一个语言表示有意义的单词。计算机使用一个编码规则，将一个字符集的成员和一个数字类型的值(比如，0=A,1=B,2=C,3=D)存储在一起。此外，当字符集排序的时候，一个collation决定了如何排序（按字母顺序排序）

默认情况下，在wordpress执行安装期间创建wordpressMYSQL数据表会使用统一编码标准utf-8字符集。从2.2版本开始，数据库字符集在wp-config.php文件中定义。同时也需要注意，用于Feed功能的字符集设置是在 [Administration](https://codex.wordpress.org/Administration_Panels) > [Settings](https://codex.wordpress.org/Administration_Panels#Reading) > [Reading panel](https://codex.wordpress.org/Settings_Reading_SubPanel).
- 参见:[collation](#collation)
- 相关文章:[Editing wp-config.php](https://codex.wordpress.org/Editing_wp-config.php) , [Converting Database Character Sets](https://codex.wordpress.org/Converting_Database_Character_Sets)
- 外部链接:[Character set at Wikipedia](https://en.wikipedia.org/wiki/Character_encoding),[Unicode at Wikipedia](https://en.wikipedia.org/wiki/Unicode),[UTF-8 at Wikipedia](https://en.wikipedia.org/wiki/UTF-8),[Character sets and collation at MySQL](https://dev.mysql.com/doc/refman/5.7/en/charset-general.html)

### chmod
chmod 是一个用于更改文件权限的 Unix/Linux shell命令。它是“change mods”的简写。

- 相关文化在哪个[Changing File Permissions](https://codex.wordpress.org/Changing_File_Permissions),[UNIX Shell Skills](https://codex.wordpress.org/UNIX_Shell_Skills),[htaccess for subdirectories](https://codex.wordpress.org/htaccess_for_subdirectories)

### class
classes是可以被任何HTML元素所引用，在css样式表中来组织样式的。在PHP中的classes，参见在维基百科中的文章[Class (Computing)](https://en.wikipedia.org/wiki/Class#Computing)和[PHP Manual: Classes and Objects.](http://php.net/manual/en/language.oop5.php).
- 相关文章:[CSS](https://codex.wordpress.org/CSS),[ Blog Design and Layout](https://codex.wordpress.org/Blog_Design_and_Layout)

### Collation <div id="collation">123123</div>
