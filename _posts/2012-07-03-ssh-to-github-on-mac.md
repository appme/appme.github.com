---
layout: post
title: "Mac上使用SSH与Github建立连接"
description: "Mac使用SSH Key与Github建立连接"
keywords: Mac,SSH,Github
category: Mac
tags: [ssh, github]
---
{% include JB/setup %}

##1.首先检查是否已有SSH Key

    $ cd ~/.ssh

如果显示`/.ssh: No such file or directory`,说明没有SSH Key,跳到第三部,如果顺利进入目录,继续.

##2.备份和移除旧的SSH Key

	$ ls
	config	id_rsa	id_rsa.pub	known_hosts
	$ mkdir key_backup
	$ cp id_rsa* key_backup
	$ rm id_rsa*

##3.生成新的SSH Key

	#用Github注册的邮箱生成SSH Key
	$ ssh-keygen -t rsa -C zhmmer@gmail.com
	Generating public/private rsa key pair.
	Enter file in which to save the key (/Users/zhm/.ssh/id_rsa): 
	Created directory '/Users/zhm/.ssh'.
	Enter passphrase (empty for no passphrase): 
	Enter same passphrase again: 
	Your identification has been saved in /Users/zhm/.ssh/id_rsa.
	Your public key has been saved in /Users/zhm/.ssh/id_rsa.pub.
	The key fingerprint is:
	3f:9e:59:f5:4c:6b:fa:e2:ed:b0:0d:c3:82:bb:3e:05 zhmmer@gmail.com
	The key's randomart image is:
	+--[ RSA 2048]----+
	|                 |
	|                 |
	|                 |
	|         E       |
	|        S .   . .|
	|         ..... +.|
	|         .+..= oo|
	|         o.=..X  |
	|        .+* .++= |
	+-----------------+

遇提示直接回车,不设密码

##4.添加SSH Key到Github

在本机设置好SSH Key后,就可以添加到Github上,建立SSH连接了

用编辑器打开`id_rsa.pub`,复制里面的所以内容
	
	zhm-mac:~ zhm$ cd .ssh
	zhm-mac:.ssh zhm$ mvim id_rsa.pub

登陆到Github主页,点击右上角的`Account Settings`设置按钮:
选择`SSH Keys`-`Add SSH key`,粘贴复制的内容,按`Add key`,提示输入登录密码后,完成添加

##5.测试连接Github是否成功

	$ ssh -T git@github.com
	The authenticity of host 'github.com (207.97.227.239)' can't be established.
	RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
	Are you sure you want to continue connecting (yes/no)?yes

输入`yes`回车,看到`Hi username! You've…`就说明连接成功了!
	
	Hi zhmme! You've successfully authenticated, but GitHub does not provide shell access.

##6.设置你的提交账号信息

现在你已经可以通过SSH链接到GitHub了,还有一些个人信息需要完善的.

Git会根据用户的名字和邮箱来记录提交,GitHub也是用这些信息来做权限的处理,输入下面的代码进行个人信息的设置,把名称和邮箱替换成你自己的,名字必须是你的真名,而不是GitHub的昵称,

	$ git config --global user.name "张慧敏"
	$ git config --global user.email zhmmer@gmail.com

####现在你可以尽情连接Github了(完)