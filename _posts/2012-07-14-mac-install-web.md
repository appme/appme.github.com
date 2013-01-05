---
layout: post
title: "Mac 安装 Web 环境"
description: "Web环境为本地测试提供了便利!"
keywords: Mac,Web
category: Mac
tags: [mac, web]
---
{% include JB/setup %}

Mac OS X 内置了Apache 和 PHP，这样使用起来非常方便。本文以Mac OS X 10.8.2为例。

##一.启动Apache

方法1.打开`系统偏好设置(System Preferences)`->`共享(Sharing)`,勾选`Web共享(Web Sharing)`,即可`启动Apache`。

注意:从Mac OS X从10.8开始取消了`Web共享(Web Sharing)`.

方法2.打开`终端(Terminal)`输入

	$ sudo apachectl start

这样Apache就启动了。

 $ sudo apachectl stop | start | restart | status

可以输入`$ apachectl -v`查看当前系统中的`Apache版本号`。

	Server version: Apache/2.2.22 (Unix)
	Server built:   Aug 24 2012 17:16:58

启动Apache后在浏览器中输入: `http://localhost` ,即可以看到 `It works!` 的页面了,它位于: `Library/WebServer/Documents/` 目录下,这就是Apache的默认目录。

注意:开启了Apache就是开启了“Web共享”，这时联网用户就会通过“http://[本地IP]/”来访问“/Library（资源库）/WebServer/Documents/”目录，通过“http://[本地IP]/~[用户名]”来访问“/Users/[用户名]/Sites/”目录。值得注意的是，Mac OS X在10.8中取消”Web共享（Web Sharing）”时，也移除了“/Users/[用户名]/Sites/”目录，所以10.8中访问“http://[本地IP]/~[用户名]”会显示“403 Forbidden”，但http://[本地IP]/依旧可以访问。可以到“系统偏好设置” -> “安全（Security）” -> “防火墙（Firewall）”，开启防火墙，然后在“防火墙选项（Firewall Options）”中勾上“组织所有进入连接（block all incoming connections）”即可。也可以通过设置httpd.conf来只允许localhost和127.0.0.1访问“/Library（资源库）/WebServer/Documents/”。

	$ sudo vi /etc/apache2/httpd.conf
	
	<Directory "/Library/WebServer/Documents">
    ......
    #
    # Controls who can get stuff from this server.
    #
    Order allow,deny
    #Allow from all
    Allow from 127.0.0.1
    Allow from localhost 

	</Directory>

##二.运行PHP

1.在终端打开Apache配置文件 输入:

	$ sudo vi /etc/apache2/httpd.conf

2.找到`#LoadModule php5_module libexec/apache2/libphp5.so`

把前面的 `#` 号去掉来开启PHP模块，保存退出(:wq!)

3.终端输入:

	$ sudo cp /etc/php.ini.default /etc/php.ini 

这样就可以通过`php.ini`来配置各种PHP功能了。

4.编辑`php.ini`可以修改参数

	$ sudo vi /etc/php.ini 
	#通过下面两项来调整PHP提交文件的最大值,如phpMyAdmin中导入数据的最大值
	post_max_size = 128M
	upload_max_filesize = 128M
	#通过display_errors来控制是否显示PHP程序的报错信息，这在调试PHP程序时非常有用
	display_errors = Off

5.重启Apache,这样PHP就设置好了

	$ sudo apachectl restart 

6.终端输入:

	$ cp /Library/WebServer/Documents/index.html.en /Library/WebServer/Documents/info.php

即在Apache的根目录下复制`index.html.en`文件并重命名为`info.php`

7.在vi中编辑	info.php	文件

	$ vi /Library/WebServer/Document/info.php

在`“It’s works!”`后面加上“`<?php phpinfo(); ?>`”，然后保存之。这样就可以在`http://localhost/info.php`中看到有关PHP的信息了。

##三.安装MySQL

由于Mac OS X中并没有预装[MySQL](http://dev.mysql.com/downloads/mysql/)，所以需要自己手动安装，目前MySQL的最稳定版本是5.6。

1.下载[MySQL 5.6](http://dev.mysql.com/downloads/mysql/5.6.html)。选择合适的版本，比如这里选择的是`mysql-5.6.5-m8-10.6-x86_64.dmg`。

2.运行dmg，会发现里面有4个文件。首先点击安装`mysql-5.6.5-m8-10.6-x86_64.pkg`，这是MySQL的主安装包。一般情况下，安装文件会自动把MySQL安装到`/usr/local`下的同名文件夹下。比如`/usr/local/mysql-5.6.5-m8-10.6-x86_64`中。一路默认安装完毕即可。

注意:从10.8开始Mac OS X的权限更加严格，直接点击会提示“mysql-5.5.27-osx10.6-x86_64.pkg can’t be opened because it is from an unidentified developer. Your security preferences allow installation of only apps from the Mac App Store and identified developers.”阻止了安装，你可以使用双指单击该安装文件，在弹出菜单中选择“用…打开（open with）”，再选择“安装（Installer）”就可以接着安装了.

3.点击安装第2个文件`MySQLStartupItem.pkg`，这样MySQL就会自动在开机时自动启动了.(注意，10.8的安装方法同上)

4.点击安装第3个文件`MySQL.prefPane`，这样就会在`系统设置偏好`中看到名为`MySQL`的ICON，通过它就可以设置MySQL开始还是停止，以及是否开机时自动运行。到这里MySQL就基本安装完毕了.(注意10.8中用双指单击该安装文件，在弹出的菜单中选择“用…打开（open with）”，然后选择“系统偏好（System Perference）”就可以接着安装了.)

5.在`bashrc配置文件`中加入`mysql`和`mysqladmin`的别名

	$ sudo vi /etc/bashrc 
	#mysql
	alias mysqlstart='sudo /Library/StartupItems/MySQLCOM/MySQLCOM restart'
	alias mysql='/usr/local/mysql/bin/mysql'
	alias mysqladmin='/usr/local/mysql/bin/mysqladmin'

这样就可以在终端中比较简单地通过命令进行相应的操作，比如安装完毕之后MySQL的root默认密码为空

6.如果要设置密码可以使用下面的命令来`设置root密码`:

 $ mysqladmin -u root password "mysqlpassword"

其中`mysqlpassword`就是密码.

或者是交互式的:

	shell> mysql -u root
	然后设置密码：
	mysql> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpwd');
	mysql> SET PASSWORD FOR 'root'@'host_name' = PASSWORD('newpwd');
	mysql> SET PASSWORD FOR 'root'@'127.0.0.1' = PASSWORD('newpwd');

其中的`host_name`是`mysql server`的`主机名`,`newpwd`是你的新密码.

或者使用UPDATE来设置密码：

	mysql> UPDATE mysql.user SET Password = PASSWORD('newpwd') WHERE User = 'root';
	mysql> FLUSH PRIVILEGES;

PS: 如果是第一次设定密码，那么使用命令:

	shell> mysql -u root

如果想重设密码，那么要加上-p选项, 并在它询问密码的时候输入当前的密码:

	shell> mysql -u root -p
    对于mysqladmin命令同样适用.
 
Anonymous帐号:

安装之后, 系统还会建立Anonymous帐号, 你可以给它设置密码也可以删除该帐号:

	shell> mysql -u root
	mysql> SET PASSWORD FOR ''@'localhost' = PASSWORD('newpwd');
	mysql> SET PASSWORD FOR ''@'host_name' = PASSWORD('newpwd');
      删除命令:
	mysql> DROP USER '';
      而下面命令删除默认与root有相同权限的Anonymous用户：
	mysql> DROP USER ''@'localhost';
	  检查用户情况：
	mysql> SELECT Host, User FROM mysql.user;
 
PS：Mac OS X的升级或者其他原因可能会导致ＭySQL启动或者开机自动运行，在ＭySQL的操作面板上会提示`Warning:The /usr/local/mysql/data directory is not owned by the 'mysql' or '_mysql'`,或者在命令行下提示`Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)`,这应该是某种情况下导致`/usr/local/mysql/data`的宿主发生了改变，只需要运行`sudo chown -R mysql /usr/local/mysql/data`即可。

另外，使用PHP连接MySQL可能会报错`Can’t connect to local MySQL server through socket ‘/var/mysql/mysql.sock’`，或者使用localhost无法连接MySQL而需要127.0.0.1，原因是连接时候php默认去找`/var/mysql/mysql.sock`了，但是MAC版本的MYSQL改动了文件的位置，放在`/tmp`下了。处理办法是按如下修改`php.ini`：

	mysql.default_socket = /tmp/mysql.sock

也可以通过`Homebrew安装`,方便快捷!

Homebrew的安装和使用见网站上的另一篇-[Mac 安装 Homebrew](/2012/07/13/mac-install-homebrew.html)

	$ brew install mysql

安装mysql会自动安装一些依赖程序比如cmake，readline，pidof，Xcode。安装完成后,按照说明执行下面代码：

	unset TMPDIR
	mysql_install_db --verbose --user=`whoami` --basedir="$(brew --prefix mysql)" --datadir=/usr/local/var/mysql --tmpdir=/tmp

启动MySQL服务

	mysql.server start

进入MySQL管理

	mysql -uroot

##四.安装phpMyAdmin

[phpMyAdmin](http://www.phpmyadmin.net/)是用PHP开发的管理MySQL的程序，非常的流行和实用。能够实用phpMyAdmin管理MySQL是检验前面几步成果的非常有效方式。

1.下载[phpMyAdmin](http://www.phpmyadmin.net/home_page/downloads.php)。选择合适的版本，比如我选择的是[phpMyAdmin-3.5.1-all-languages.tar.bz2](http://sourceforge.net/projects/phpmyadmin/files/phpMyAdmin/3.5.1/phpMyAdmin-3.5.1-all-languages.tar.bz2/download#!md5!06bb0b8a945e114e767dfaec67dc5ae0)这个版本。

2.终端cd到`phpMyAdmin-3.5.1-all-languages.tar.bz2`所在目录,输入:

	$ tar jxvf phpMyAdmin-3.5.1-all-languages.tar.tar.bz2 #解压,然后cd进入解压目录
	$ cd phpMyAdmin-3.5.1-all-languages #拷贝创建phpmyadmin配置文件config.inc.php
	$ cp config.sample.inc.php config.inc.php 
	$ vi config.inc.php #做如下修改:
	$cfg['blowfish_secret'] = 'a9b8c7d'; /* 用于Cookie加密，随意的长字符串 */
	$cfg['Servers'][$i]['auth_type'] = 'http';  # 延长登录时间
	$cfg['Servers'][$i]['host'] = '127.0.0.1'; # 把localhost 改为 127.0.0.1
	$cfg['Servers'][$i]['AllowNoPassword'] = false; # 把false改成true，这样就可以访问无密码的MySQL了

PS:当phpMyAdmin中出现`#2002 无法登录 MySQL 服务器`时，请把`localhost`改成`127.0.0.1`就ok了，这是因为MySQL守护程序做了IP绑定`bind-address =127.0.0.1`造成的 `$cfg['Servers'][$i]['host'] = 'localhost'`;

3.保存退出,然后把`phpMyAdmin-3.5.1-all-languages`文件夹名`改名`为`phpmyadmin`并移动到`/Library/WebServer/Documents`目录中。
 
	$ sudo mv phpMyAdmin-3.5.1-all-languages /Library/WebServer/Documents/phpyadmin

4.把`phpyadmin` link到webserver上

把下载的phpMyAdmin-3.5.1-all-languages 放到自己的某个目录下,如:

	/usr/local/system/phpMyAdmin-3.5.1-all-languages

把phpmyadmin link到webserver上

	$ cd  /Library/WebServer/Documents
	$ sudo ln -nfs /usr/local/system/phpMyAdmin-3.5.1-all-languages /Library/WebServer/Documents/phpmyadmin

这样就可以通过`http://localhost/phpmyadmin`访问`phpMyAdmin`了。这个时候就看到一个提示`无法加载 mcrypt 扩展，请检查您的 PHP 配置。`，这就涉及到下一节安装MCrypt扩展了。

##五.配置PHP的MCrypt扩展库

[MCrypt](http://mcrypt.sourceforge.net/)是一个功能强大的加密算法扩展库，它包括有22种算法，phpMyAdmin依赖这个PHP扩展库。但是它在Mac OS X下的安装却不那么友善，具体如下：

1.下载并解压[libmcrypt-2.5.8.tar.bz2](http://sourceforge.net/projects/mcrypt/files/Libmcrypt/)。

2.在终端执行如下命令（注意如下命令需要安装xcode支持）：

	$ cd ~/Downloads/libmcrypt-2.5.8/
	$ ./configure
	$ make
	$ sudo make install

Autoconf错误安装解决:
	
	cd ~/Downloads/libmcrypt-2.5.8/
	curl -O http://ftp.gnu.org/gnu/autoconf/autoconf-latest.tar.gz
	tar xvfz autoconf-latest.tar.gz
	cd autoconf-2.69/
	./configure
	make
	sudo make install

3.下载并解压PHP源码文件[php-5.3.15.tar.bz2](http://us2.php.net/get/php-5.3.15.tar.bz2/from/a/mirror)。Mac OS X 10.8.2中预装的PHP版本是5.3.15,你需要依据自己的实际情况选择对应的版本。

4.在终端执行如下命令：

	cd ~/Downloads
	tar -zxvf php-5.3.15.tar.bz2
	cd php-5.3.15/ext/mcrypt
	curl -O http://ftp.gnu.org/gnu/autoconf/autoconf-latest.tar.gz
	tar xvfz autoconf-latest.tar.gz
	cd autoconf-2.69/
	./configure
	make
	sudo make install
	
	cd ..
	phpize

Configuring for:
PHP Api Version:         20090626
Zend Module Api No:      20090626
Zend Extension Api No:   220090626
configure.in:3: warning: prefer named diversions
configure.in:3: warning: prefer named diversions

	./configure
	make
	sudo make install

Installing shared extensions:     /usr/lib/php/extensions/no-debug-non-zts-20090626/

5.打开php.ini:

	$ sudo vi /etc/php.ini

在php.ini中加入如下代码，并保存后退出，然后重启Apache

	extension=mcrypt.so

6.重启Apache:

	sudo apachectl restart

当你再访问http://localhost/phpmyadmin时，会发现“无法加载 mcrypt 扩展，请检查您的 PHP 配置。”提示没有了，这就表示MCrypt扩展库安装成功了。如果还不能加载，尝试把php.ini中的加入的extension修改为：

	extension=/usr/lib/php/extensions/no-debug-non-zts-20090626/mcrypt.so

##六.设置虚拟主机

1.终端打开Apche的配置文件

	$ sudo vi /etc/apache2/httpd.conf

在httpd.conf中找到`#Include /private/etc/apache2/extra/httpd-vhosts.conf`”，去掉前面的`＃`，保存并退出。

2.终端`重启Apache`后就开启了它的虚拟主机配置功能。

	$ sudo apachectl restart 
 
3.终端打开配置虚拟主机的文件`httpd-vhost.conf`

	$ sudo vi /etc/apache2/extra/httpd-vhosts.conf

配置你需要的虚拟主机了。需要注意的是该文件默认开启了两个作为例子的虚拟主机：

	<VirtualHost *:80>
    	ServerAdmin webmaster@dummy-host.example.com
    	DocumentRoot "/usr/docs/dummy-host.example.com"
    	ServerName dummy-host.example.com
    	ErrorLog "/private/var/log/apache2/dummy-host.example.com-error_log"
    	CustomLog "/private/var/log/apache2/dummy-host.example.com-access_log" common
	</VirtualHost>
	<VirtualHost *:80>
    	ServerAdmin webmaster@dummy-host2.example.com
    	DocumentRoot "/usr/docs/dummy-host2.example.com"
    	ServerName dummy-host2.example.com
    	ErrorLog "/private/var/log/apache2/dummy-host2.example.com-error_log"
    	CustomLog "/private/var/log/apache2/dummy-host2.example.com-access_log" common
	</VirtualHost>

而实际上，这两个虚拟主机是不存在的，在没有配置任何其他虚拟主机时，可能会导致访问localhost时出现如下提示：

	Forbidden
	You don't have permission to access /index.php on this server

最简单的办法就是在它们每行前面加上#，注释掉就好了，这样既能参考又不导致其他问题。(修改后需重启Apache生效)
 
增加如下配置

	<VirtualHost *:80>
		DocumentRoot "/Library/WebServer/Documents"
		ServerName localhost
		ErrorLog "/private/var/log/apache2/localhost-error_log"
		CustomLog "/private/var/log/apache2/localhost-access_log" common
	</VirtualHost>

	<VirtualHost *:80>
		DocumentRoot "/Volumes/Web/WWW/Drupal"
		ServerName Drupal
		ErrorLog "/private/var/log/apache2/Drupal-error_log"
		CustomLog "/private/var/log/apache2/Drupal-access_log" common
		<Directory />
				Options Indexes FollowSymLinks MultiViews
				AllowOverride All
				Order deny,allow
				Allow from all
		</Directory>
	</VirtualHost>


保存退出,并重启Apache.

	$ sudo apachectl restart
 
5.终端打开hosts配置文件

	$ sudo vi /etc/hosts

加入`127.0.0.1 Drupal`，这样就可以配置完成`Drupal 虚拟主机`了，这样就可以用`http://Drupal`访问了，其内容和`http://localhost/~[用户名]`完全一致。

##启用Mod Rewrite和.htaccess

Apache的Mode Rewrite模块提供了一个基于正则表达式分析器的重写引擎来实时重写URL请求。在大多数情况下，它和.htaccess文件配合使用。比如本篇文章的URL（http://zhm.me/2012/07/14/mac-install-web-environment.html）就是Wordpress配合Mod Rewrite模块和.htaccess文件一起实现的,即所谓的固定链接（Permalinks）。

1.在终端运行sudo vi /etc/apache2/httpd.conf，找到#LoadModule rewrite_module modules/mod_rewrite.so，去掉前面的注释符号#。

2.运行sudo vi /etc/apache2/extra/httpd-vhost.conf，加入

	<Directory "/Users/[用户名]/Sites">
		Options Indexes FollowSymLinks MultiViews
		AllowOverride All
		Order allow,deny
		Allow from all
	</Directory>

这样整个~/Sites都可以支持.htaccess。

3.运行 sudo vi /Private/etc/apache2/users/[用户名].conf，把其中的AllowOverride None改成AllowOverride All。需要注意的是，以前的Mac OS X版本，路径可能是/private/etc/httpd/users/[用户名].conf

4.在需要的目录新建.htaccess，并修改其权限为777

	cd /Volumes/Web/WWW/Drupal
	touch .htaccess
	chmod 777 .htaccess

新建文件的权限默认是644，通过ls -l .htaccess就可以看到，此时程序无法自动写入.htaccess，这种情况比较安全，但是需要手动写入。

5.退出后重启Apache：sudo apachectl restart

完成上述设置之后，就可以使用固定链接功能了。需要注意的是，如果.htaccess是从Windows下直接复制过来，日志中可能会出现</IfModule> without matching <IfModule> section的报错。简单的解决方案就是新建文件，重新复制粘贴。

当然了，你还可以使用`MAMP`来配置开发环境，这个就相对比较简单了，里面集成的apache、mysql、phpmyadmin。

问题1:在安装Drupal时,到连接数据库时出现
"Warning: PDO::__construct(): [2002] No such file or directory(trying to connect via unix:///tmp/mysql.sock) in ..."错误,主机名用:127.0.0.1可以解决

问题2:目录权限设置 $ sudo chmod -R 777 language/

打开终端输入：

	sudo mvim /etc/apache2/httpd.conf

运行上面的命令以后会要求输入 root 账户密码，密码正确的话会打开 vi。找到下面两行：

	User _www
	Group _www

再把这两行改成：

	User 你的Mac用户名
	Group staff

按 esc 键，在输入双引号内的字符”:qw”和回车保存推出，重启 Apache 服务。以后升级 WordPress 的时候，主机填 127.0.0.1，用户名填你的 Mac 用户名，密码填写 Mac 的用户密码即可顺利升级WordPress。

问题3:Mac本地安装WordPress,开启固定链接设置后,网站目录无权限访问了,系统已经自动生成.htaccess 文件,如果把此文件删除或把里面的内容清空,网站都可以正常访问,可以判断应该是规则设置有问题,参考Joomla的.htaccess后得出结论:需要在最上面添加一行

	Options +FollowSymLinks
	
	## Mod_rewrite in use.
	# BEGIN WordPress

WorldPress再自动生成别的规则也回保留这条,问题解决了!搞了半天一直以为是权限的问题.