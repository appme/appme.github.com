---
layout: post
title: "Mac下利用goagent免费翻墙"
description: "Mac下利用goagent免费翻墙"
keywords: Mac,goagent
category: Mac
tags: [goagent]
---
{% include JB/setup %}

##第一步:申请appengine

登录[http://appengine.google.com](http://appengine.google.com),申请帐号,已有gmail帐号就不必注册

##第二步:创建Application

1：顺利登录后，点击`Create Application`

![Creat an Application](http://i.imgur.com/dIPAX.png)

2：接着国家选择`Other(Not Listed)`,输入你的手机号码

![Verify Your Account by SMS](http://i.imgur.com/puwBm.png)

+86 格式如:+8613888888888,点send提交.几秒后,谷歌会发来短信(免费的),里面有一串数字,填上即可.

3.点击send后,Google App Engine账号即被激活,然后就可以创建新的应用程序了.页面会自动转入`My Applications`页面,点击`Create an Application`新建应用

![Create an Application](http://i.imgur.com/2DRtt.png)

`Application Identifier`需要为字母开始,不能有下划线和中划线,可以包含数字

4.创建成功后跳转到`Application Registered Successfully`页面

![Application Registered Successfully](http://i.imgur.com/T9Gq3.png)

5.至此,你已经完成了一个应用的申请,现在强烈建议不要关闭网页,转到`http://appengine.google.com`页面,一口气把剩下的9个应用也一起申请.因为最近很多朋友反映,关闭网页后再回到谷歌申请应用时,会要求再次验证手机,但是谷歌并不会发送验证短信.这也许是个bug.

问：为什么要创建这么多应用？

答：一个Gmail账户最多可以创建十个Google App Engine应用。每个应用每天有1GB免费流量，10个应用每天就有10GB的流量，这就是有备无患的意思。比如你经常看youtube的视频，1GB 的流量大概只能支撑3小时，用完了，就可以换第2个应用继续看了。

结果如下

![My Applications](http://i.imgur.com/f21M2.png)

##第三步:创建2步验证

通过这2步才可以收到提交应用需要的密码,应用都发布完成后,这个手机验证可以去掉,不然每次登录gmail都需要手机验证码

1.登录`https://accounts.google.com`,点击`安全性`两步验证`修改`

![两步验证](http://i.imgur.com/UOHLB.png)

2.点击`使用两步验证`,在新的页面`设置两步验证`.输入`手机号`后点击`发送验证码`,接着你会收到一条验证短信,里面有数字,填上`验证码`确认.最后点击`下一步`,直到`启用两步验证`按钮结束

![设置两步验证](http://i.imgur.com/q7RgP.png)

3.点击“创建密码”或回到https://accounts.google.com 点击`向应用程序和网站授权`后的`修改`进行密码的创建

![创建密码](http://i.imgur.com/DunkO.png)

4.在`第 1 步（共 2 步）：生成新的应用专用密码`

输入`名称`后点`生成密码`

![生成密码](http://i.imgur.com/HEJi8.png)

5.记录生成的密码,等会用到

![记录生成的密码](http://i.imgur.com/RW5GL.png)

##第四步:下载goagent客户端

http://code.google.com/p/goagent/

goagent 1.8.11 稳定版下载 [http://goo.gl/pTt0W](http://goo.gl/pTt0W)

MAC下进行解压,可以解压到用户根目录下,比如`/Users/admin/goagent`

修改`server\python\app.yaml`把`your_appid`改你的`appid`,用于提交这个ID的应用到google appengine上

![app.yaml](http://i.imgur.com/9zWYZ.png)

cd到server目录下,运行`$ python uploader.zip update ./`

会提示输入`gmail帐号`和`前面生成的密码`(不是你google邮箱的密码哦)

提交成功后,登录`http://appengine.google.com`,会看到应用已经发布

以此类推,把10个都提交上去,最好10个应用都已经发布了

修改local\proxy.ini中的[gae]下的appid=你的appid(多appid请用|隔开 appid=id1|id2|id3)

上传完服务端并设置好`proxy.ini`之后,在终端直接运行`python proxy.py`即可.需要Python版本2.6以上.

Mac用户可以尝试`[GoAgent Mac GUI](http://code.google.com/p/goagent/downloads/detail?name=GoAgentMac.dmg&can=2&q=)`

打开该包以后,拖到Application目录下,但是还需要修改goagent的路径,需要进入该目录,找到该应用程序的图标,然后显示包内容进去,修改

`GoAgentMac.app/Contents/Info.plist`eg:`/Users/admin/local/proxy.py`,然后运行即可. 

这样代理就开通了,IP为127.0.0.1,端口为8087

`chrome`请安装[SwitchySharp](https://chrome.google.com/webstore/detail/dpplabbmogkhghncfbfdeeokoefdjegm)插件,然后导入这个设置`http://goagent.googlecode.com/files/SwitchyOptions.bak`

主要就是将代理地址和端口添加进去,保存即可

`firefox`请安装`FoxyProxy`,Firefox需要导入证书,方法请见FAQ

###该网站的安全证书不受信任！解决办法

Mac下,`前往`-`实用工具`-`钥匙串访问`-`证书`导入`/Users/admin/local/CA.crt`证书,并双击`GoAgent CA`,信任设置成`总是信任`,把所有证书都设置成`总是信任`,完成!