<span id="Linux">跳转到的地方</span>
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
