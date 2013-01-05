---
layout: post
title: "Drupal7 添加底部友情链接区块"
description: "Drupal7 添加底部友情链接区块"
category: Drupal
tags: [drupal]
---
{% include JB/setup %}

在`管理界面`依次点:`admin(管理)/structure(结构)/block(区块)`

在 `区块` 界面 点 `添加区块` 添加一个`Block区块`

`区块标题` 可不填 `区块描述` 填(`友情链接`) `区块内容` 填入你的友情链接源码如:

	<a href="http://www.zikercn.com/" target="_blank" title="紫客网">紫客网</a> | 
	<a href="http://bbs.zikercn.com/" target="_blank" title="紫客论坛">紫客论坛</a> | 
	<a href="http://blog.zikercn.com/" target="_blank" title="张慧敏官方博客">张慧敏官方博客</a> |
	<a href="http://t.zikercn.com/" target="_blank" title="张慧敏官方微博">张慧敏官方微博</a>

`文本格式` 选择:`Full HTML`

`区域设置` 指定此区块在哪些主题和区域中显示。
（`默认主题`）选择 `页脚` , `保存区块` 完成。

####(完)