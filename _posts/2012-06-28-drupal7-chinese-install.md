---
layout: post
title: "Drupal7 中文安装教程"
description: "Drupal7 中文安装教程"
keywords: drupal,教程
category: Drupal
tags: [drupal]
---
{% include JB/setup %}

1.到[Drupal官网](http://drupal.org)下载最新版的[Drupal7](http://drupal.org/project/drupal),解压上传至你的网站目录.

2.到Drupal官网,下载对应版本的简体中文语言包[drupal-7.13.zh-hans.po](http://localize.drupal.org/translate/languages/zh-hans)上传至“`profiles/standard/translations/`”目录下.

3.浏览器中输入`你的网址`,进入`安装页面`:默认选中`Standard`,点击 `Save and continue`执行下一步.

4.选择语言:选中`Chinese, Simplified (简体中文)`,点击`Save and continue`执行下一步.

5.数据库设置:填写数据库的配置配置信息,包括`数据库类型`、`数据库名`、`数据库用户名`、`数据库用户密码`

如果数据库主机在别的服务器上要在`高级`选项中填写,公共数据库最好加上 `表前缀`,之后点击`保存并继续`开始安装Drupal7.

6.之后进入自动`按设置安装`相应模块,自动`安装翻译`导入语言包.

如遇到`导入翻译出错`(原因是执行超时了)有两种解决办法:

`方法一`:修改`php.ini`文件：`memory_limit = 256M` (依实际情况设定)
删除 `sites/default/settings.php` 删除数据库,重新安装.

`方法二`:打开`\sites\default\settings.php`文件(删除旧的,复制default.settings.php改为settings.php创建新的)，在最后增加以下两行：

	ini_set('memory_limit' , '256M'); //加大php的内存 也可以在php.ini中设置
	ini_set('max_execution_time' , 2000); //加大页面执行时间 php.ini中的默认值是30 (秒)

删除数据库,重新安装.

7.站点设置：在站点设置页面，填写`网站名称`、`网站邮箱`、`超级管理员帐号`、`超级管理员邮箱`、`超级管理员密码`、`默认时区`和`简洁链接`，配置完成之后，点击"`保存并继续`"即完成 `Drupal` 的安装,进入完成信息提示页面,点击"`访问你的新网站`"链接即可访问你的`Drupal站点!`

**Drupal7如果安装的是英文版,如何汉化成中文版?**

1.到[Drupal官网](http://drupal.org/)下载对应版本的简体中文语言包([drupal-7.13.zh-hans.po](http://localize.drupal.org/translate/languages/zh-hans))稍后备用.

2.`管理` 点击 `Modules` 到`模块面板`,找到 `Locale` 模块(默认已启动),如果未启动勾选前面的复选框,点击下面的 `Save Configuration` 按钮 保存.

3.`管理` 点击 `Configuration/Translate interface/IMPORT` 点 `Language file` 选择刚才下载的(`drupal-7.13.zh-hans.po`)文件,`Import into` 选择`Chinese, Simplified(简体中文)`,点下面的 `Import` 按钮导入

4,`管理`点击 `Configuration/Languages` 选中 `Chinese, Simplifie “简体中文”`语言项后面的 `DEFAULT单选项`，点击下面的保存 `Save Configuration` 按钮,完成!
