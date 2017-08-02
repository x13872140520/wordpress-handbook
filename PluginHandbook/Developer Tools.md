#### Developer Tools
这里有很多有用的工具来帮助插件开发。他们其中的一些运行在你的开发环境(xdebug.PHPCS等等)，还有一些非常好的工具在wordpress内运行，来帮助你正确的构造一些东西，以及诊断问题。这章介绍的是浏览器工具。

#### Debug Bar以及相关组件
##### Debug Bar
Debug Bar 这个插件被启用时，会在wordpress后台管理栏中添加一个菜单，来显示请求，缓存，还有其他有用的调试信息。

当启用WP_DEBUG时，它还可以监控PHP的警告(Warnings)和注意(Notices),使其容易得被找到。

SAVEQUERIES被启用时，会监控和显示出mysql查询。

[点击查看 Debug Bar](https://wordpress.org/plugins/debug-bar/)

##### Debug Bar Console
Debug Bar Console这个插件提供了一个很大的文本域让你可以运行任意的PHP，这在测试变量等的内容中是非常有用的.

[点击查看 Debug Bar Console](https://wordpress.org/plugins/debug-bar-console/)

##### Debug Bar Shortcodes
Debug Bar Shortcodes这个插件给Debug Bar增加了一个新的面板来显示当前请求的已注册的简码。
此外它可以为你显示:
- 简码调用的哪个函数/方法。
- 简码是否用在了当前的 post/page发布类型中，以及它们如何被使用（仅仅在用单简码情况下）
- 任何关于简码的额外信息，比如描述，用到的参数，是不是可以自闭合。
- 找出所有用到了简码的页面/文章等等。

[点击查看 Debug Bar Shortcodes](https://wordpress.org/plugins/debug-bar-shortcodes/)
##### Debug Bar Constants
Debug Bar Constants给Debug Bar添加了三个新面板来显示当前请求中那些已被定义，你这个开发者可以使用的常量。

##### Debug Bar Post Types
Debug Bar Post Types给Debug Bar添加了一个面板来显示你网页中已经注册的发布类型的相关信息的细节。

[点击查看 Debug Bar Post Types](https://wordpress.org/plugins/debug-bar-post-types/)

##### Debug Bar Cron
Debug Bar Cron在Debug Bar里添加了关于WP scheduled events（wordpress预定事件）的相关信息的面板。这个插件是Debug Bar的一个扩展，因此，它依赖于Debug Bar，只有Debug Bar被安装好了，它才能正常工作。
一旦安装成功，你可以访问以下信息:
- 预定事件的数量
- 当前cron是否运行
- 下一个事件的事件
- 当前时间
- 自定义预定事件的清单
- 核心预定事件的清单
- 计划清单

[点击查看Debug Bar Cron](https://wordpress.org/plugins/debug-bar-cron/)

##### Debug Bar Actions and Filters Addon
这个插件在调试栏中添加了两个选项卡，用来显示连接到当前请求的钩子(动作和过滤器)。Actions(动作)选项卡显示了当前请求的动作钩子。Filters(过滤器)选项卡显示了过滤器标签以及与之相关的功能。

[点击查看 Debug Bar Actions and Filters Addon](https://wordpress.org/plugins/debug-bar-actions-and-filters-addon/)

##### Debug Bar Transients
Debug Bar Transients给Debug Bar添加了关于WordPress Transients信息的新面板。这个插件是Debug Bar的一个扩展，因此，它依赖于Debug Bar，只有Debug Bar被安装好了，它才能正常工作。
一旦安装成功，你可以访问以下信息:
- 目前存在的transients的数量
- 自定义的transients的清单
- 核心transients的清单
- 自定义站点transients的清单
- 核心站点transients的清单
- 一个删除transients的选项

[点击查看 Debug Bar Transients](https://wordpress.org/plugins/debug-bar-transients/)

##### Debug Bar List Script & Style Dependencies
列出加载的脚本和样式，加载它们的顺序，以及存在的依赖项。

[点击查看 Debug Bar List Script & Style Dependencies](https://wordpress.org/plugins/debug-bar-list-dependencies/)

##### Debug Bar Remote Requests
这将通过HTTP API来记录和配置远程请求。
这个插件会给Debug Bar添加一个“远程请求”面板来显示:
- 请求的方法(GET,POST等等)
- URL
- 每个请求的时间
- 所有请求的总时间
- 所有请求的数量

根据情况，你可以往你的URL中添加类似?dbrr_full=1来获取额外的包含了所有请求的参数，完整的响应头信息。

[点击查看 Debug Bar Remote Requests](https://wordpress.org/plugins/debug-bar-remote-requests/)

#### 辅助插件
##### Query Monitor
对于任何使用WordPress的人来说，Query Monitor是一个调试插件。您可以在数据库查询、钩子、条件语句、HTTP请求、重定向等方面查看调试和性能信息。它有一些其他调试插件无法使用的高级特性，包括自动的AJAX调试，以及通过插件或主题来省事的能力。
