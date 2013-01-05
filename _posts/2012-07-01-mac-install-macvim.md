---
layout: post
title: "Mac上安装MacVim与配置"
description: "这篇文章备忘macvim的安装macvim的配置,为重装系统可以快速把必要的工具装上"
keywords: Mac,MacVim
category: Mac
tags: [mac, macvim]
---
{% include JB/setup %}

##MacVim下载安装

Download [MacVim 7.3 (snapshot 64) for Mac OS X Lion](https://github.com/downloads/b4winckler/macvim/MacVim-snapshot-64.tbz "MacVim 7.3 (snapshot 64) for Mac OS X Lion"). (Released Jan 2, 2012.)

下载后得到`MacVim-snapshot-64.tbz`这个包里面有三个文件（`MacVim`、`mvim`、`reader.txt`）

把`MacVim.app`放到你的`应用程序`也就是`/Applications`目录下

**PS**:必须放到`应用程序`目录下,否则终端调用:`mvim` 会找不到MacVim的可执行文件

把`mvim`拷贝到`/usr/bin/`这个目录下

	$sudo cp -f mvim /usr/bin/

终端就可以通过`$ mvim 文件名` 来启动`MacVim`编辑文件了

`reader.txt`看完删除

__PS__:如果不想吧`MacVim`装到`应用程序(Applications)`目录下,又想在终端调用`mvim`,可以编辑`/etc/bashrc`文件(`$ sudo vim /etc/bashrc`),将以下代码添加到文件中 `:wq!` 强制保存退出)

	alias mvim='/Volumes/App/App/MacVim.app/Contents/MacOS/MacVim'

##配置.vimrc

打开`MacVim-Edit-Startup Settings`,打开`~/.vimrc`,添加配置,保存即可

在终端输入`$ vi`在`vi编辑器`中输入`:version`可以查看系统中`vimrc的位置`

	system vimrc file: "$VIM/vimrc"  『注:vimrc系统配置文件位置』
	user vimrc file: "$HOME/.vimrc"  『注:vimrc用户配置文件位置』

如果不知道`$VIM`或`$HOME`具体是哪个目录,可以在`vi`中用下面的命令查看:

	:echo $VIM (/usr/share/vim)
	:echo $HOME (/Users/zhm 就是用户终端的根目录)

用户配置文件内容会覆盖系统配置文件内容,所以编辑用户配置文件就可以了

终端输入:

	$ vim ~/.vimrc

打开添加配置内容后用`:wq!`强制保存退出

##安装配色or插件

安装配色或插件前,先建好必要的`.vim`相关目录

	:~$ mkdir .vim
	$ cd .vim
	$ mkdir after autoload colors compiler doc ftplugin indent keymap plugin syntax

###配色文件

下载配色文件(`lucius.vim`)拷贝到`colors`目录中

	:.vim zhm$ cp /Users/zhm/Downloads/lucius.vim colors

然后在`.vimrc`中加入:`colorscheme lucius`,就可以了

###ZenCoding-vim

下载`ZenCoding-vim`后,拷贝两个文件到目录,重新打开`vim`就可以使用了`Ctrl+y+,`

拷贝`plugin/zencoding.vim`到`~/.vim/plugin`目录.

拷贝`autoload/zencoding.vim`到`~/.vim/autoload`目录

[Download zip file](http://www.vim.org/scripts/script.php?script_id=2981)

	cd ~/.vim
	unzip zencoding-vim.zip

或者克隆安装
	
	git clone http://github.com/mattn/zencoding-vim.git
	cd zencoding-vim
	cp plugin/zencoding.vim ~/.vim/plugin/
	cp autoload/zencoding.vim ~/.vim/autoload/

打开或创建一个新文件:

	vim index.html

插入模式输入`html:5`然后按快捷键`Ctrl+y+','`你将看到:

	<!DOCTYPE HTML>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title></title>
	</head>
	<body>
	    _
	</body>
	</html>

##小技巧

####删除行尾空格
行末:`$`	
行首:`^`	
空格:`\s`		
行末空格:`\s\+$`	
行首空格:`^\s\+`	

	删除行尾多个空格 : %s/\s\+$//g
	删除行首多个空格 : %s/^ \+//g