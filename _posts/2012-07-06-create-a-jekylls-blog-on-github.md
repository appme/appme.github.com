---
layout: post
title: "使用Github Pages创建基于Jekyll的博客"
description: "这篇文章介绍的是使用Github Pages服务+Jekyll模板引擎来搭建自己的个人博客"
keywords: Github,Pages
category: Github
tags: [jekyll, github]
---
{% include JB/setup %}


##1.建立一个特殊的Repository

前往你的[Github][],以你的`用户名`新建一个名称如:`zhmme.github.com`的空项目

##2.安装Jekyll-Bootstrap

	$ git clone https://github.com/plusjade/jekyll-bootstrap.git zhmme.github.com
	$ cd zhmme.github.com
	$ git remote set-url origin git@github.com:zhmme/zhmme.github.com.git
	$ git push origin master

在Github上一两分钟后,你的博客就可以访问了[http://zhmme.github.com](http://zhmme.github.com)

##3.安装Jekyll本地环境

以本地浏览你的博客,你需要用`ruby gem`安装`Jekyll`,依赖的模块也会被自动安装

	$ gem install jekyll

如果在安装时遇到问题,请参考<<[Mac上安装与更新Ruby,Rails运行环境](/2012/07/ruby-and-rails-on-mac.html)>>更新运行环境

安装完Jekyll后,还需要安装`RDiscount`,因为RDiscount里面包含markdown语法包,安装如下:

	$ sudo gem install rdiscount

在你网站下的`_config.yml`文件中加入已下配置

	markdown: rdiscount

安装成功后,就可以进入刚刚克隆的`zhmme.github.com`,启动`Jekyll`自带迷你服务器

	$ cd zhmme.github.com 
	$ jekyll --server 

你的博客现在可以可以本地访问了: [http://localhost:4000/](http://localhost:4000/)
或: [http://0.0.0.0:4000/](http://0.0.0.0:4000/)

##4.创建一篇日志

发布日志前,先在配置文件`_config.yml`中设置`URL`格式
	
	permalink: /:year/:month/:title.html

其他格式参考: https://github.com/mojombo/jekyll/wiki/Permalinks

	$ rake post title="Hello World"
	Creating new post: ./_posts/2012-07-02-hello-world.md

##5.创建一个页面

	$ rake page name="about.md"
	Creating new page: ./about.md
	创建一个嵌套的页面
	$ rake page name="pages/about.md"
	Creating new page: ./pages/about.md
	创建一个路径页面
	$ rake page name="pages/about"
	Creating new page: ./pages/about/index.html

Jekyll也提供了许多预设的页面例子,以供参考.你可以学习和按自己的需要自定义它.

[Archive](/archive.html "存档")
[Categories](/categories.html "分类")
[Pages](/pages.html "页面")
[Tags](/tags.html "标签")

##6.发布

当你添加`日志`,`页面`或改变你的主题或其他文件,只需将它们提交给你的`git`Push提交到`GitHub`.

	$ git add .
	$ git commit -m "Add new content"
	$ git push origin master

##7.绑定域名

`Github`为我们提供了绑定独立域名的服务,配置也很简单

只有在`Github`你的博客知识库中添加一个包含你的域名的`CNAME`文件,然后做好域名`DNS`的`A`记录,等待生效就可以了!

我的域名注册在`Godaddy`,但它的DNS服务有点慢,我选择了国内的[DNSPod](https://www.dnspod.cn/ "DNSPod")服务,可参考DNSPod的帮助文档:`https://www.dnspod.cn/Support`

在`原域名注册商`处修改`DNS`服务:如`Godaddy`修改`Nameservers`为这两个地址:`f1g1ns1.dnspod.net`,`f1g1ns2.dnspod.net`.如果你不明白在哪里修改，可以参考这里:[各个注册商修改DNS地址的方法](https://www.dnspod.cn/support/index/fid/1#2 "各个注册商修改DNS地址的方法")

在`DNSPod`自己的域名下添加一条`A记录`,地址是`Github Pages`的`IP地址`,`204.232.175.78`,可`ping`得到

	$ ping pages.github.com
	PING pages.github.com (204.232.175.78): 56 data bytes

等待域名解析生效,然后在`项目根目录`添加一个包含你的域名的`CNAME`文件:

	$ echo "zhm.me" > CNAME
	$ git add .
	$ git commit -m "Add CNAME"
	$ git push origin master
	$ jekyll --server

等待`GitHub`处理解析生效,这大约需要`10分钟`,以后就可以用你的顶级域名[ZHM.ME](http://zhm.me/ "张慧敏")访问你在`GitHub`上的`博客`了!

##8.小技巧

###git删除远程文件

直接删除或改名本地文件,远程却没有删除或重新创建了一个文件,处理办法

用`git rm`命令,再删除一次,即使本地已经没有这个文件了

	$ git rm _posts/core-samples/2011-12-29-jekyll-introduction.md
	rm '_posts/core-samples/2011-12-29-jekyll-introduction.md'
	$ git commit -m 'delete'
	[master f5c7489] delete
	 1 files changed, 0 insertions(+), 411 deletions(-)
	 delete mode 100644 _posts/core-samples/2011-12-29-jekyll-introduction.md
	$ git push origin master

这样就可以在远程也删除了





[Github]:   http://github.com "Github"