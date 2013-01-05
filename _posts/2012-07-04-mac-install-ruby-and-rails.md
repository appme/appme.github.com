---
layout: post
title: "Mac上安装与更新Ruby,Rails运行环境"
description: "本地安装`Jekyll`环境时遇到`Ruby`版本低,通过本篇就可以解决"
keywords: Mac,Ruby,Rails
category: Mac
tags: [ruby, gem, rvm]
---
{% include JB/setup %}

Mac安装后就安装`Xcode`是个好主意,它将帮你安装好Unix环境需要的开发包,也可以独立安装`command_line_tools_for_xcode`

##1.安装RVM

RVM:Ruby Version Manager,Ruby版本管理器,包括Ruby的版本管理和Gem库管理(gemset).

	$ curl -L get.rvm.io | bash -s stable
	或者
	$ bash -s stable < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)

等待一段时间后就可以成功安装好RVM,

	$ source /Users/zhm/.rvm/scripts/rvm
	$ source ~/.bashrc
	$ source ~/.bash_profile

测试是否安装正确

	$ rvm -v
	rvm 1.14.5 (stable) by Wayne E. Seguin <wayneeseguin@gmail.com>, Michal Papis <mpapis@gmail.com> [https://rvm.io/]

##2.用RVM安装Ruby环境

	$ ruby -v #查看当前ruby版本
	ruby 1.8.7 (2011-12-28 patchlevel 357) [universal-darwin11.0]
	$ rvm list known #列出已知的ruby版本
	$ rvm install 1.9.3 #安装ruby 1.9.3

完成以后,`Ruby,RubyGems`就安装好了.

Ruby如果安装错版本可以卸载

	$ rvm list #查询已经安装的ruby
	=* ruby-1.9.3-p194 [ x86_64 ]
	$ rvm remove 1.9.3 #卸载一个已安装版本

##3.设置Ruby默认版本

用RVM装好Ruby以后,需要执行下面的命令将指定版本的Ruby设置为系统默认版本

	$ rvm use 1.9.3 --default
	Using /Users/zhm/.rvm/gems/ruby-1.9.3-p194

查看设置后的默认ruby版本和gem版本

	$ ruby -v
	ruby 1.9.3p194 (2012-04-20 revision 35410) [x86_64-darwin11.4.2]
	$ gem -v
	1.8.24

如果需要更新`gem`(RubyGems)可以用命令

	$ gem update --system
	Updating RubyGems
	ERROR:  http://rubygems.org/ does not appear to be a repository
	ERROR:  While executing gem ... (Gem::RemoteFetcher::FetchError)
    timed out (http://rubygems.org/yaml)

由于国内网络原因`你懂的`,导致`rubygems.org`存放在`Amazon S3`上面的资源文件间歇性连接失败.所以你会与遇到`gem install rack`或`bundle install`的时候半天没有响应,具体可以用`gem install rails -V`来查看执行过程。

解决办法使用 [Rubygems 镜像 - 淘宝网](http://ruby.taobao.org/)

	$ gem sources -l #列出
	*** CURRENT SOURCES ***

	http://rubygems.org/
	$ gem sources -a http://ruby.taobao.org/ #添加
	http://ruby.taobao.org/ added to sources
	$ gem sources -r http://rubygems.org/ #移除
	http://rubygems.org/ removed from sources
	$ gem sources -l #列出
	*** CURRENT SOURCES ***
 
	http://ruby.taobao.org #请确保只有ruby.taobao.org,有其他再用第一条移除
	$ gem install rack #安装个rack测试

可以清除旧的`gem`版本

	$ gem cleanup

##4.安装Rails环境

上面3步过后,Ruby环境就安装好了,接下来安装Rails

	$ gem install bundler rails

然后测试安装是否正确

	$ bundle -v
	Bundler version 1.1.4
	$ rails -v
	Rails 3.2.6

####现在可以本地安装`Jekyll`环境了

	$ gem install jekyll