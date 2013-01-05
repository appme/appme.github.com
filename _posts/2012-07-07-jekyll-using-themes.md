---
layout: post
title: "Jekyll主题定制"
description: "JB版本0.2.x主题现在完全模块化。他们跟踪和版本单独作为主题包。这让大家自由发布和共享主题。"
keywords: Github,jekyll
category: Github
tags: [jekyll]
---
{% include JB/setup %}

##介绍

`JB版本0.2.x`主题现在完全模块化。他们跟踪和版本单独作为`主题包`。这让大家自由发布和共享主题。

`Jekyll-Bootstrap v 0.2.x`自带`twitter`的主题。其他主题需要`安装`

`Jekyll-Bootstrap` 使用`rake tasks`命令实现主题的安装与切换。

##寻找主题

你可以在官方的[主题管理](http://themes.jekyllbootstrap.com/)页面找到和浏览最新的官方主题。

此外你也可以开发和发布自己的主题,只要他们符合标准,你也可以用相同的方法安装你的主题.

GitHub上直接浏览目前的主题包：[https://github.com/jekyllbootstrap](https://github.com/jekyllbootstrap)

##安装主题`themes`

安装主题使用`rake`与主题的`git地址`
	
	$ rake theme:install git="https://github.com/jekyllbootstrap/theme-the-program.git"

安装使用`Git下载`的主题包,或者另一种方式获得的`zip`主题包,你都可以手动放置到您的`/_theme_packages`文件夹,然后运行安装的主题名称。

	$ rake theme:install name="主题名称"

安装成功后系统会提示你是否想要切换到新安装的主题,输入`Y`确认切换

##切换主题`_includes`

一旦你的主题安装完毕后，你可以在它们之间切换，通过`rake	`命令：

	$ rake theme:switch name="THEME-NAME"

主题文件目录`./_includes/themes/主题名称`,这是主要的主题目录,而不是在编辑`_layouts`内的主题文件,因为`切换`主题将覆盖`_layout`目录下的文件内的连接,这样做是保持主题模块化,这种方式编辑一个不影响其他。

##样式脚本文件`assets`

样式脚本文件目录`./assets/themes/主题名称`,包含每个`主题`的样式文件。他们在`./assets/themes/主题名称`。确保您编辑和添加这个目录中的`样式`。所有的主题都提供了路径变量`ASSET_PATH`链接至上述目录。

	<link rel="stylesheet" href="{{ASSET_PATH}}/css/style.css">

##Jekyll Bootstrap API

你的主题应该尽可能使用JB API.`_includes/JB/API名称`

`JB/analytics`JB/分析,应始终包括在default.html和结束标记前
	
	{ % include JB/analytics % }
	</body>

`JB/comments`JB/注释,应始终包括在post.html文件,即使你不支持注释,它应该是由用户通过配置设置禁用的意见.

	...
	  <div id="post">
	    {{content}}
	  </div>
	  <div class="comments">
	    { % include JB/comments % }
	  </div>
	...

##添加您自己的主题

阅读官方[主题API文档](http://jekyllbootstrap.com/api/theme-api.html)查看如何建立和发布`Jekyll Bootstrap`自定义主题的说明。
