---
layout: post
title: "Mac 安装 Wget"
description: "GNU Wget是一个在网络上进行下载的简单而强大的自由软件，其本身也是GNU计划的一部分。它的名字是“World Wide Web”和“Get”的结合，同时也隐含了软件的主要功能。目前它支持通过HTTP、HTTPS，以及FTP这三个最常见的TCP/IP协议协议下载。"
keywords: Mac,Wget
category: Mac
tags: [wget]
---
{% include JB/setup %}

##Wget下载
下载地址HTTP:[http://ftp.gnu.org/gnu/wget/](http://ftp.gnu.org/gnu/wget/)

下载地址FTP:[ftp://ftp.gnu.org/gnu/wget/](ftp://ftp.gnu.org/gnu/wget/)

下载wget-1.13.4.tar.gz到Downloads/

##Wget安装

1.cd到wget-1.13.4.tar.gz的目录,输入
	
	$ tar zxvf wget-1.13.4.tar.gz #解压(bz2文件解压命令: $ tar jxvf wget-1.13.4.tar.bz2)


2.cd进入解压到的wget-1.13.4目录,输入 

	$ ./configure

3.一般会报这个错：

	configure: error: --with-ssl was given, but GNUTLS is not available.
	添加参数 $ ./configure --with-ssl=openssl 

顺利完成!

4.然后输入: 

	$ make

根据makefile制定的规则，将c\c++文件编译成*.o文件，然后进一步生成可执行文件。

5.接着输入:

	$ sudo make install

6.输入密码完成安装! 

	可以输入:$ make clean

删除源代码（C\C++ code）生成的执行文件和所有的中间目标文件

##Wget使用

测试下载输入:

	$ wget www.baidu.com 测试是否安装成功

成功下载百度首页index.html到了当前目录下！

	$ /Users/zikercn/Downloads/wget-1.13.4/index.html

Wget的命令格式如下：`wget [options] [URL]`

	$ wget -r -np -nd http://example.com/packages/
这条命令可以下载 http://example.com 网站上 packages 目录中的所有文件。其中，-np 的作用是不遍历父目录，-nd 表示不在本机重新创建目录结构。

	$ wget -r -np -nd --accept=iso http://example.com/centos-5/i386/
与上一条命令相似，但多加了一个 --accept=iso 选项，这指示 wget 仅下载 i386 目录中所有扩展名为 iso 的文件。你也可以指定多个扩展名，只需用逗号分隔即可。

	$ wget -i filename.txt
此命令常用于批量下载的情形，把所有需要下载文件的地址放到 filename.txt 中，然后 wget 就会自动为你下载所有文件了。

	$ wget -c http://example.com/really-big-file.iso
这里所指定的 -c 选项的作用为断点续传。

	$ wget -m -k (-H) http://www.example.com/
该命令可用来镜像一个网站，wget 将对链接进行转换。如果网站中的图像是放在另外的站点，那么可以使用 -H 选项。

####Wget卸载删除