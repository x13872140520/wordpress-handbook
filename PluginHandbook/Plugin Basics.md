#### 插件基础
#### 开始吧
最简单的，一个wordpress插件是一个有着wordpress头部注释的PHP文件。极力推荐你创建一个文件夹来放置你的插件，这样你所有的插件文件将会整齐的被组织在一个地方。

来开始创建一个新的插件吧，跟着下面这些步骤:
1. 导航到您的WordPress的wp-content安装目录。
2. 打开plugin文件夹。
3. 在已有的插件后创建一个新文件夹并命名(如:plugin-name)
4. 进入你的新的插件文件夹
5. 创建一个新的PHP文件(最好给这个文件命名，如plugin-name.php)

这是在Unix命令行中看到的进程:
```
wordpress$ cd wp-content
wp-content$ cd plugins
plugins$ mkdir plugin-name
plugins$ cd plugin-name
plugin-name$ vi plugin-name.php
```
在上面的例子中，'VI'是文本编辑器的名字，用适合你的编辑器。

现在你正在创建你的新插件的php文件，你将需要添加一个插件头注释。这是一个指定格式的，包含了你插件的相关信息的PHP块注释，比如它的名字和作者。最起码的，插件头注释必须要写你的插件的名字。在你插件的文件下的唯一的文件必须要有头注释-如果你的插件有多个PHP文件，仅仅需要一个文件有这个头注释就行。

```
<?php
/*
Plugin Name: YOUR PLUGIN NAME
*/
```
保存文件之后，你应该可以在你的wordpress页面的中看到你的插件了。登录你的wordpress后台管理，点击左边的导航面板的插件选项。这个页面显示了你当前wordpress拥有的所有插件列表。你的新插件应该在里面了。

#### 钩子函数:动作和过滤器
wordpress钩子允许你在某些特定的点上，不通过编辑任何核心文件就可以改变wordpress行为。

在wordpress下有两种类型的钩子，actions(动作)和filters(过滤器)。动作允许你添加或者修改wordpress的功能，然而过滤器允许你修改已经加载的并显示给wordpress用户的内容。

钩子不仅仅用于插件开发，在wordpress核心提供默认功能时，钩子被广泛的用到。其他的钩子是未使用的，当你需要修改wordpress的工作方式时，你可以简单的，直接使用它们。这就是为什么wordpress如此灵活的原因。

#### 基本钩子
当你创建插件的时候你需要用到3个基本的钩子，它们是
- [register_activation_hook()](https://developer.wordpress.org/reference/functions/register_activation_hook/)
- [register_deactivation_hook()](https://developer.wordpress.org/reference/functions/register_deactivation_hook/)
- [register_uninstall_hook()](https://developer.wordpress.org/reference/functions/register_uninstall_hook/)

当你启用你的插件的时候，激活钩子[activation hook](https://developer.wordpress.org/plugins/the-basics/activation-deactivation-hooks/)在运行.你会用到它来提供一个功能来设置你的插件-比如，在选项表中创建某些默认设置。

当你停用你的插件的时候，注销钩子[deactivation hook](https://developer.wordpress.org/plugins/the-basics/activation-deactivation-hooks/)在运行，你将会使用它来清除存储在你的插件中的临时数据。

这些未安装方法[uninstall methods](https://developer.wordpress.org/plugins/the-basics/uninstall-methods/)被用于清除，在你使用wordpress后台管理删除了你的插件之后。你将会用它来删除所有由你的插件产生的数据，比如添加到选项表中的任何选项。

#### 添加钩子
你可以通过[do_action()](https://developer.wordpress.org/reference/functions/do_action/)来添加属于你自己的自定义的钩子，这样使开发者们能够通过你的钩子函数传递函数来扩展你的插件。

#### 移除钩子
你也可以通过调用[remove_action()](https://developer.wordpress.org/reference/functions/remove_action/)来移除之前定义的函数。比如，如果你的插件是另一个插件的附属组件，你可以和上一个插件用[ add_action()](https://developer.wordpress.org/reference/functions/add_action/)添加的同样的回调函数一起用remove_action()
