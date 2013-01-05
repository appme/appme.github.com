---
layout: post
title: "用Github建个人博客(Win环境)"
description: "不喜欢新浪腾讯网易等网站提供的博客环境,希望手动建立自己的博客,把博客掌控在自己的手中,Github就可以给我们提供这样一个机会.
"
keywords: Win,Jekyll
category: Github
tags: Win jekyll
---
{% include JB/setup %}

许多人跟我一样,喜欢把自己的工作,学习和生活中的点滴写成文章发表到网上,与朋友分享,博客成了一个非常好的选择,但是如果你还像我一样,懂一点点网络基础,又不喜欢新浪腾讯网易等网站提供的博客环境,希望手动建立自己的博客,把博客掌控在自己的手中,Github就可以给我们提供这样一个机会.

[Github](https://github.com/)本身是一个版本库管理网站,许多大公司如:facebook,twitter,microsoft,vmware,redhat,mozilla都有项目托管在Github上,所以我们完全可以信赖!他提供了一个[Github Pages](http://pages.github.com/)服务,用WEB页面展示项目的介绍,并且可以帮绑定独立域名!这就让我们可以变相的做成我们需要的免费稳定的博客站点了!

Github Pages有以下几个优点:

- 轻量级的博客系统,没有麻烦的配置
- 使用标记语言,比如[Markdown](http://markdown.tw/)
- 无需自己搭建服务器
- 根据Github的限制,对应的每个站有300MB空间
- 可以绑定自己的域名

当然他也有缺点：

- 使用[Jekyll](http://jekyllrb.com/)模板系统,相当于静态页发布,适合博客,文档介绍等. * 动态程序的部分相当局限,比如没有评论,不过还好我们有解决方案.
- 基于Git,很多东西需要动手,不像Wordpress有强大的后台

大致介绍到此,作为个人博客来说,简洁清爽的表达自己的工作、心得,就已达目标,所以Github Pages是我认为此需求最完美的解决方案了.

##WIN下使用Github

1.首先当然是要注册一个Github账号啦!

2.Windows下连接Github要下载一个[Git客户端](http://code.google.com/p/msysgit/downloads/list),下载[Git-1.8.0-preview20121022.exe](http://msysgit.googlecode.com/files/Git-1.8.0-preview20121022.exe)的最新版本安装好就可以了.

3.在桌面或开始菜单找到*Git Bash*打开,首先需要检查电脑上是否已有SSH Key:

	$ cd ~/.ssh

如果显示/.ssh: No such file or directory,说明没有SSH Key,跳到第5步,如果顺利进入目录,继续.

4.备份和移除旧的SSH Key

	$ ls
	config  id_rsa  id_rsa.pub  known_hosts
	$ mkdir key_backup
	$ cp id_rsa* key_backup
	$ rm id_rsa*

5.生成新的SSH Key

用Github注册的邮箱生成SSH Key,然后一路回车下去.

	$ ssh-keygen -t rsa -C zhmmer@gmail.com

6.添加SSH Key到Github

用编辑器打开id_rsa.pub,路径在`C:\Users\HP\.ssh\id_rsa.pub`复制里面的所以内容

登陆到Github主页,点击右上角的Account Settings设置按钮: 选择SSH Keys-Add SSH key,粘贴复制的内容,按Add key,提示输入登录密码后,完成添加

7.输入下面命令测试连接Github是否成功

	$ ssh -T git@github.com

如果出现下面的提示,输入`yes`回车.

	The authenticity of host 'github.com (207.97.227.239)' can't be established.
	RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
	Are you sure you want to continue connecting (yes/no)?yes

输入yes回车,看到Hi username! You've…就说明连接成功了!

	Hi zhmme! You've successfully authenticated, but GitHub does not provide shell access.

8.设置你的提交账号信息
现在你已经可以通过SSH链接到GitHub了,还有一些个人信息需要完善的.

Git会根据用户的名字和邮箱来记录提交,GitHub也是用这些信息来做权限的处理,输入下面的代码进行个人信息的设置,把名称和邮箱替换成你自己的,名字必须是你的真名,而不是GitHub的昵称,

	$ git config --global user.name "zhm"
	$ git config --global user.email zhmmer@gmail.com

现在你可以尽情连接Github了(完)

##使用GitHub Pages建立博客

1.与GitHub建立好链接之后,就前往Github,用你的`用户名`新建一个名如:`zhmme.github.com`的空项目.

2.克隆一个Jekyll-Bootstrap项目到本地,然后再push到你的远程`zhmme.github.com`

	$ git clone https://github.com/plusjade/jekyll-bootstrap.git zhmme.github.com
	$ cd zhmme.github.com
	$ git remote set-url origin git@github.com:zhmme/zhmme.github.com.git
	$ git push origin master

在Github上一两分钟后,你的博客就可以访问了http://zhmme.github.com

如果是更新已有的项目,那就把远程的项目先克隆到本地

	$ git clone git@github.com:zhmme/zhmme.github.com.git

克隆成功后.cd到zhmme.github.com目录下

	$ cd zhmme.github.com

##Win上搭建Jekyll本地测试环境

Windows平台的用户,下载安装GitHub的客户端,[GitHub for Windows](http://windows.github.com/)是一个100%的本地应用,可以运行在 Windows XP,Vista,7 & 8.应用中包括完整的[msysGit](http://msysgit.github.com/)安装(同[Cygwin](http://cygwin.com/setup.exe)一样是一个Windows下的Linux模拟环境),使其成为在Windows上使用Git的不二选择。(安装需要.Net Framework 4,在线下载,ssh会重新自动安装)

下载最新的[RubyInstaller](http://rubyforge.org/frs/?group_id=167)并安装(我下载的是[rubyinstaller-1.9.3-p327.exe](http://rubyforge.org/frs/download.php/76557/rubyinstaller-1.9.3-p327.exe))，如果需要可以在命令行终端下输入gem update --system来升级gem

下载最新的[DevKit](https://github.com/oneclick/rubyinstaller/downloads/)(我下载的是[DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe](https://github.com/downloads/oneclick/rubyinstaller/DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe))并双击运行解压到C:\DevKit。然后打开终端cmd，输入下列命令进行安装：

	cd C:\DevKit
	ruby dk.rb init
	ruby dk.rb install

PS:DevKit是windows平台下编译和使用本地C/C++扩展包的工具。它就是用来模拟Linux平台下的make,gcc,sh来进行编译。但是这个方法目前仅支持通过RubyInstaller安装的Ruby。

完成上面的准备就可以安装Jekyll了,因为Jekyll是用Ruby编写的,最好的安装方式是通过RubyGems(gem):

	gem install jekyll

并使用命令jekyll --version检验是否安装成功

一般而言，还可以安装Rdiscount，这个用来解析Markdown标记的包，使用如下命令：

	gem install rdiscount

现在,Jekyll的本地环境就配置完成了.

下面我们先使用pizn.github.com的blog仓库做示例代码,点击其页面上的Clone in Windows按钮，就会调用你之前安装好的GitHub客户端，将该仓库的代码下载到本地。默认位置是我的文档下的GitHub文件夹内。

让我们在本地测试看看下载得到的pizn博客站点是否可以成长运行。

打开终端命令行，CD进入到你clone得到的pizn.github.com目录下，运行以下命令：

	jekyll --server --auto

打开浏览器，输入 http://127.0.0.1:4000 进行访问。

如果遇到浏览器错误提示

	no access permission to `/'

不能生成静态页面,可能是Jekyll读取文件时的默认编码问题

解决方案:
修改Jekyll读取文件时的默认编码,在Jekyll安装目录的convertible.rb文件中,我的安装位置是:

	C:\Ruby193\lib\ruby\gems\1.9.1\gems\jekyll-0.11.2\lib\jekyll

将convertible.rb文件中的第27行（左右）由

	self.content = File.read(File.join(base, name))

修改为

	self.content = File.read(File.join(base, name), :encoding => 'utf-8')

重新开启server,如果出现类似下面的:

	Liquid error: invalid byte sequence in GBK
	liquid error: incompatible character encodings: UTF-8 and GBK 

通过修改系统环境变量的方式来解决这一问题,即在命令提示符下输入:

	set LC_ALL=en_US.UTF-8
	set LANG=en_US.UTF-8

现在Jekyll的本地Server正常启动。
