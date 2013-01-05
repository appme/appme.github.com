---
layout: post
title: "Mac 安装 MacPorts"
description: "MacPorts，曾经叫做DarwinPorts，是一个软件包管理系统，用来简化Mac OS X和Darwin操作系统上软件的安装。它是一个用来简化自由软件/开放源代码软件的安装的自由/开放源代码项目，与Fink和BSD类ports套件的目标和功能类似。跟BSD中的ports道理一样。MacPorts就像apt-get、yum一样，可以快速安装些软件。"
keywords: Mac,MacPorts
category: Mac
tags: [mac]
---
{% include JB/setup %}

##MacPorts安装

一.通过(`.pkg`)安装: Mac OS X Package (.pkg) Installer

访问官方网站: [http://www.macports.org/install.php](http://www.macports.org/install.php)

[http://distfiles.macports.org/MacPorts/MacPorts-2.1.1-10.7-Lion.pkg](http://distfiles.macports.org/MacPorts/MacPorts-2.1.1-10.7-Lion.pkg)

二.通过(`Source`)安装MacPorts：Source Installation

1.cd到`Downloads`目录,`wget`下载 MacPorts-2.1.1.tar.gz 输入: 

	$ wget https://distfiles.macports.org/MacPorts/MacPorts-2.1.1.tar.gz

2.解压 MacPorts-2.1.1.tar.gz 输入:

	$ tar zxvf MacPorts-2.1.1.tar.gz (tar jxvf MacPorts2.1.1.tar.bz2)

3.cd到解压到的目录MacPorts-2.1.1输入:

	$ ./configure && make && sudo make install #安装

中间提示输入密码完成安装!

4.然后将/opt/local/bin和/opt/local/sbin添加到$PATH搜索路径中
编辑/etc/profile文件 

	$ sudo vim /etc/profile
	#(特许编辑,强制保存退出 wq!)文件最后加上下面两句
	export PATH=/opt/local/bin:$PATH
	export PATH=/opt/local/sbin:$PATH

##MacPorts使用

1.MacPort中第三方软件下载包存放的默认路径是:`/opt/local/var/macports/distfiles/`
为了提高安装速度，可以在安装新port时直接将此目录下的文件拷贝到新的MacPort相同的目录中就可以避免Port去网上下载。

2.使用MacPort前应该首先更新Port的index 输入: 

	$ sudo port -v selfupdate
	#(强烈推荐第一次运行的时候使用-v参数，显示详细的更新过程)

3.查看Mac Port中当前可用的软件包及其版本 输入: 
	
	$ port list

4.查看有更新的软件以及版本 输入: 

	$ port outdated

5.升级可以更新的软件 输入: 

	$ sudo port upgrade outdated

6.在MacPort搜索需要安装的软件包 比如`maven`输入: 

	$ port search maven
	maven @1.0.2 (java, devel)
    	stub port, use maven1 instead

	maven-ant-tasks @2.1.3 (devel, java)
    	Use many of Maven's artifact handling features from Ant.

	maven1 @1.1 (java, devel)
    	A java-based build and project management environment.

	maven2 @2.2.1 (java, devel)
    	A java-based build and project management environment.

	maven3 @3.0.4 (java, devel)
    	A java-based build and project management environment.

	maven_select @0.3 (sysutils)
    	common files for selecting default Maven version

	Found 6 ports.

7.搜索到需要安装的软件包之后，如何查看具体的软件包的内容和说明 输入: 

	$ port info maven3

	maven3 @3.0.4 (java, devel)
 
	Description:      Maven is a Java project management and project
                      comprehension tool. Maven is based on the concept of a
                      project object model (POM) in that all the artifacts
                      produced by Maven are a result of consulting a well
                      defined model for your project.Builds, documentation,
                      source metrics, and source cross-references are all
                      controlled by your POM. Maven 3 aims to ensure backward
                      compatibility with Maven 2, improve usability, increase
                      performance, allow safe embedding, and pave the way to
                      implement many highly demanded features.
	Homepage:             http://maven.apache.org/
 
	Build Dependencies:   kaffe
	Runtime Dependencies: maven_select
	Platforms:            darwin
	License:              unknown
	Maintainers:          blair@macports.org, gk5885@kickstyle.net

8.查看即将安装的或者已经安装的软件包的依赖关系 输入: 

	$ port deps maven3
	Full Name: maven3 @3.0.4_0
	Build Dependencies:   kaffe
	Runtime Dependencies: maven_select

9.查看安装时允许客户定制的参数 输入: 

	$ port variants maven3
	maven3 has no variants

10.查看了软件包的内容和说明,并确认确实要安装,则输入: 

	$ sudo port install maven3
	To make maven 3.0.4 the default, please run
	    sudo port select --set maven maven3
 
	--->  Cleaning maven3
	--->  Updating database of binaries: 100.0%
	--->  Scanning binaries for linking errors: 100.0%
	--->  No broken files found.

11.卸载已经用Mac Port安装的软件 输入: 

	$ sudo port uninstall maven3
	--->  Deactivating maven3 @3.0.4_0
	--->  Cleaning maven3
	--->  Uninstalling maven3 @3.0.4_0
	--->  Cleaning maven3

##MacPorts卸载删除

卸载原有的MacPorts(如果你没有安装,直接跳过这一步,输入: `$ port version` 查看)

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

####(完)
