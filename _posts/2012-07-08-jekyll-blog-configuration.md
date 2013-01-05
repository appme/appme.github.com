---
layout: post
title: "Jekyll博客配置"
description: "Jekyll提供了博客的永久固定链接定制选项"
keywords: Github,Jekyll
category: Github
tags: [jekyll]
---
{% include JB/setup %}

##发布博客的路径格式

Jekyll提供了博客的永久固定链接定制选项,你可以参考这里的格式表：[Jekyll永久链接](https://github.com/mojombo/jekyll/wiki/Permalinks)

Jekyll-Bootstrap,默认的URL固定链接格式:

	permalink: /:categories/:year/:month/:day/:title/

结构包含`分类`加上`日期`和最后的`标题`构成,你可以配置你想要的URL格式.

##设置BASE_PATH

预计将与前面的BASE_PATH在哲基尔引导所有职位和网页网址
设置`BASE_PATH`为`Jekyll-Bootstrap`使用的全局路径

BASE_PATH配置是特殊情况下,在您的博客必须从一个分目录运行。主要情况是,如果你的博客将托管在GitHub的项目页。如果您正在部署GitHub的项目之一，这个网站，你必须设置BASE_PATH的 GitHub项目名称。

在任何情况下，你可以离开这个空白，如果你定义为您的网站的CNAME。更多的信息是：http://pages.github.com

PS:在`localhost`时，您的网站将运行从`根目录/`开始,而无视`BASE_PATH`。

##启用评论

Jekyll-Bootstrap使用部件代码启用的评论包括 [Disqus](http://disqus.com/), [Intense Debate](http://intensedebate.com/), [livefyre](http://www.livefyre.com/)和 [Facebook Comments](https://developers.facebook.com/docs/reference/plugins/comments/)

为使你的博客有评论系统,你需要选择这些供应商之一,并注册帐户。在`_config.yml`你应该看到评论`comments`的设置部分如下所示：

	# Settings for comments helper
	# Set 'provider' to the comment provider you want to use.
	# Set 'provider' to false to turn commenting off globally.
	#
	comments :
	  provider : disqus
	  disqus :
    short_name : jekyllbootstrap
	  livefyre :
    site_id : 123
	  intensedebate :
    account : 123abc
	  facebook :
    appid : 123
    num_posts: 5
    width: 580
    colorscheme: light    

**选择提供商**

设置`provider`为您打算使用的供应商。确保名为哈希内的相关供应商指定的帐户凭据，供应商。

在上面的例子中使用了`disqus`与供应商提供的`SHORT_NAME`帐户`jekyllbootstrap`

**使用自定义评论程序**

使用自定义评论程序，设置提供商为`provider: custom`。接下来在这个路径下创建一个文件

	./_includes/custom/comments
	
该文件将加载任何主题包括其意见，所以你可以通过这个文件注入你自己的widget代码。

**禁用评论**

设置`provider: false`可以禁用全部评论功能

禁用指定`页面/日志`的评论,则在指定的`页面/日志`中设置`comments: false`

	--- 
	layout: post
	category : lessons
	comments : false
	tags : [yay]
	---

##启用Analytics（分析）

`Jekyll-Bootstrap`可以包含的网站分析的代码包括[Google](http://google.com/analytics)和[GetClicky](http://getclicky.com/)提供的。

为了启用您的博客的分析,你会需要选择这些供应商之一，已设置帐户。在`_config.yml`找到对应的分析`analytics`设置代码如下所示：


	# Settings for analytics helper
	# Set 'provider' to the analytics provider you want to use.
	# Set 'provider' to false to turn analytics off globally.
	#        
	analytics :
	  provider : google
	  google : 
      tracking_id : 'UA-123-12'
	  getclicky :
	    site_id :
**选择提供商**

设置`provider`为您打算使用的供应商。确保名为哈希内的相关供应商指定的帐户凭据，供应商。

在上面的例子，使用了`google`与google提供的`tracking_id : UA-123-12`

**使用自定义提供程序**

使用自定义提供程序，设置服务提供商`provider: custom`接下来,在以下路径创建一个文件

	./_includes/custom/analytics

该文件将加载任何主题的分析，所以你可以通过这个文件注入你自己的widget代码。

##禁用分析

设置供应商`provider: false`禁用全部分析。

禁用指定`页面/日志`的评论,则在指定的`页面/日志`中设置`analytics: false`

	---
	layout: post
	category : lessons
	analytics : false
	tags : [yay]
	---

####博客的大概配置`完`