#### 插件开发的介绍
欢迎来到插件开发手册。不论你正开发的是第一个还是第50个插件，我们希望这个资源能够尽可能的帮助你写出最好的插件。

插件开发手册涵盖了一系列的要点-插件的头部所需要的每个部分，怎样遵循最佳实践，构建你的插件所需要使用的工具。这也是一个正在进行的工作-如果你发现什么遗漏和未完成的，请帮忙完善它。

wordpress有三个主要的组件:
- core
- themes
- plugins

这个手册解释了wordpress插件以及它们如何相互影响，它将会帮助你理解它们如何工作，怎么创建它们。

#### 我们为什么写插件

因为在wordpress开发中，有一条红线不可触动，那就是:绝对不要碰wordpress core。这就意味着你不能通过修改核心来给你的网页增加功能。这是因为，当wordpress更新到一个新的版本，它就会重写所有核心文件。因此，你想添加任何功能就必须通过wordpress APIs所批准的插件来实现。

wordpress插件根据你的需要，和你想做的事情，可以既简单又复杂。最简单的插件就是一个php文件，这个[Hello Dolly](https://wordpress.org/plugins/hello-dolly/)插件就是这么一个例子。这个PHP文件插件仅仅需要一个插件头，一对PHP函数，和一些钩子函数来引入你的函数。

插件允许你不触及wordpress核心来大大扩展wordpress的功能。

#### 插件是什么？
插件是扩展了wordpress核心功能的代码包。wordpress插件是由PHP代码和其他资源比如图片，CSS，javascript。

扩展wordpress可以通过制作你自己的插件，比如，在wordpress已经提供了的基础上构建额外的功能。举个例子，你可以写一个插件来在你的网页中显示最近新添加的10篇文章的链接。

又或者，使用wordpress的自定义文章类型，你可以写一个插件来创建一个功能齐全的，支持售票系统，邮件通知，自定义票据，还有客户端，这可能性是无限的。

大多数wordpress插件往往由很多文件构成，但是一个插件仅仅需要在一个主要的文件有指定格式的头部就行[DocBlock](https://en.wikipedia.org/wiki/PHPDoc#DocBlock).

[Hello Dolly](https://wordpress.org/plugins/hello-dolly/).第一个插件，仅仅只有82行代码。Hello Dolly在wordpress管理中显示了[the famous song](https://en.wikipedia.org/wiki/Hello,_Dolly!_(song))的歌词.一些CSS文件被用在PHP文件中，来控制歌词显示的样式。

作为一名wordpress.org官方插件作者，你有一个很好的机会来创建一个将要被安装，被修补，被数百万的wordpress用户所爱的插件，你仅需要将你的想法变成代码。这个插件手册将会帮你做到。
