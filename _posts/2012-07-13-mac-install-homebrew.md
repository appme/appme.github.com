---
layout: post
title: "Mac 安装 Homebrew"
description: "Homebrew是一个Ruby开发的智能的包管理系统。她能判断系统包的状况，并能够依赖系统已有的组件，不用重新下载一阵套组件,独特式的解决了包的依赖问题。而MacPorts是自成一派的,他的所有组件全部安装在/opt目录下，带来的问题就是很多系统已经有的组件都要重新下载，费时间也费空间。而且Homebrew本身使用Git管理，升级非常方便。并不再需要烦人的sudo，一键式编译，无参数困扰。支持千余种开源软件在 Mac OS X 中的部署和管理。"
keywords: Mac,Homebrew
category: Mac
tags: [mac]
---
{% include JB/setup %}

##Homebrew安装

Homebrew 项目托管在 Github 上

[http://mxcl.github.com/homebrew](http://mxcl.github.com/homebrew)

[https://github.com/mxcl/homebrew](https://github.com/mxcl/homebrew)

现在你的Mac已经完全可以从`MacPorts`中解脱出来，完全拥抱`Homebrew`.(它们之间是不兼容的)

1.卸载原有的MacPorts,如果你没有安装,直接跳过这一步,输入: 

	$ port version 查看是否安装了

原版使用MacPorts安装过的软件在`/opt/local`目录下,删除之前最好查看下,心里有个数.

	$ sudo port -f uninstall installed
	$ sudo rm -rf  [/加下面的每条]
	/opt/local
	/Applications/DarwinPorts
	/Applications/MacPorts
	/Library/LaunchDaemons/org.macports.* 
	/Library/Receipts/DarwinPorts*.pkg 
	/Library/Receipts/MacPorts*.pkg 
	/Library/StartupItems/DarwinPortsStartup
	/Library/Tcl/darwinports1.0 
	/Library/Tcl/macports1.0 
	~/.macports

2.安装Homebrew

(1)首先确保你电脑上已经安装了`xcode`,这点灰常重要。

(2)终端执行(不建议sudo)：

	$ ruby -e "$(/usr/bin/curl -fsSL https://raw.github.com/mxcl/homebrew/master/Library/Contributions/install_homebrew.rb)"

(3)没有三，已经完成了，查看版本号可以终端执行：

	$ brew -v

##Homebrew使用

搜索软件包wget(假定只知道get):

	$ brew search get

安装wget:

	$ brew install wget

卸载wget:

	$ brew uninstall wget

列出已经安装包:

	$ brew list

查看某软件包安装的详细路径和安装内容:

	$ brew list wget

更多帮助请看:

	$ man brew

查看brew的帮助:

	$ brew help

显示包依赖:

	$ brew deps wget

更新软件:

	$ brew update #把所有的Formula目录更新并且会对本机已经安装并有更新的软件用*标明

更新某个软件:

	$ brew upgrade git

查看软件信息:

	$ brew info git | brew home git (用浏览器打开)

删除程序,和upgrade一样,单个软件删除和所有程序老版删除.

	$ brew cleanup git | brew cleanup

查看哪些已安装的程序需要更新:

	$ brew outdated

*Homebrew*将本地的`/usr/local`初始化为git的工作树,并将目录所有者变更为当前所操作的用户,以后的操作将不需要sudo。

Homebrew的主程序安装在`/usr/local/bin/brew`中,在目录`/usr/local/Library/Formula/`下保存了Homebrew支持的所有软件的安装指引文件。

使用Homebrew方式安装，`Git`被安装在`/usr/local/Cellar/git/<version>/`中,可执行程序自动在`/usr/local/bin`目录下创建符号连接,可以直接在终端程序中访问。

	-bin          用于存放所安装程序的启动链接（相当于快捷方式）
	-Cellar       所以brew安装的程序，都将以[程序名/版本号]存放于本目录下
	-etc          brew安装程序的配置文件默认存放路径
	-Library      Homebrew 系统自身文件夹
	+–Formula     程序的下载路径和编译参数及安装路径等配置文件存放地
	+–Homebrew    brew程序自身命令集

##Homebrew卸载删除

万一你用的不爽了,告诉你卸载指令:

	$ cd `brew –prefix`
	$ rm -rf Cellar
	$ brew prune
	$ rm -rf Library .git .gitignore bin/brew README.md share/man/man1/brew
	$ rm -rf ~/Library/Caches/Homebrew

另外,你已经安装了git了,那么建立了本地的git仓库,执行如下:

	$ cd /usr/local
	$ git init
	$ git remote add origin git://github.com/mxcl/homebrew.git
	$ git pull origin master

如果GitHub上有项目,也可直接拿下:

	$ git clone http://github.com/YOURGITHUBUSERNAME/homebrew.git /tmp/homebrew
	
	
	
	
	
	