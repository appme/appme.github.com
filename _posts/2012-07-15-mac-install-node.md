---
layout: post
title: "Mac 安装 Node 环境"
description: "Node.js 是一个服务器端 JavaScript 解释器，它将改变服务器应该如何工作的概念。它的目标是帮助程序员构建高度可伸缩的应用程序，编写能够处理数万条同时连接到一个（只有一个）物理机的连接代码。"
keywords: Node,Mac
category: Mac
tags: [node, mac]
---
{% include JB/setup %}


##Node.js安装

在Mac下,用简单的`Homebrew`来安装,不会Homebrew的看[Mac中Homebrew安装和使用](/2012/07/mac-install-homebrew.html)

	$ brew install node

安装完成node，会提示你没有安装npm，并告诉你具体的安装办法。

	Homebrew has NOT installed npm. We recommend the following method of
	installation:
	  curl http://npmjs.org/install.sh | sh
 
	After installing, add the following path to your NODE_PATH environment
	variable to have npm libraries picked up:
	  /usr/local/lib/node_modules

安装npm

	$ curl http://npmjs.org/install.sh | sh

安装成功如下$ npm -v 查看版本

	make: Nothing to be done for `doc'.
	/usr/local/bin/npm -> /usr/local/lib/node_modules/npm/bin/npm-cli.js
	npm@1.1.24 /usr/local/lib/node_modules/npm
	It worked

设置NODE_PATH环境变量

	$ export NODE_PATH="/usr/local/lib/node_modules/"

测试

	$ vi example.js

	var http = require('http');
 
	http.createServer(function (request, response) {
        response.writeHead(200, {'Content-Type': 'text/plain'});
        response.end('Hello World!\n');
    }).listen(8888);
 
	console.log('Server running at http://127.0.0.1:8888/');

	$ node example.js
	Server running at http://127.0.0.1:8888/

测试显示**`Hello World!`**成功!

安装express框架(由于这个有点特殊，需要为npm添加-g参数，刚开始安装的时候没有加，导致不能使用epress 命令行参数)

	$ npm install -g express
	express默认使用jade view engine，所以在安装jade 
	#npm install jade
	$ epxress -v #看看是否安装成功

	其他引擎有： 
	    Haml haml implementation 
	    Jade haml.js successor 
	    EJS Embedded JavaScript 
	    CoffeeKup CoffeeScript based templating 
	    jQuery Templates for node 
	如果需要，请用npm安装

新建一个Node server文件夹~/node_server

	$ cd ~
	$ mkdir node_server
	$ cd node_server

在里面创建项目nodetest测试

	:node_server zikercn$ express nodetest
 
	   create : nodetest
	   create : nodetest/package.json
	   create : nodetest/app.js
	   create : nodetest/public
	   create : nodetest/public/javascripts
	   create : nodetest/public/images
	   create : nodetest/public/stylesheets
	   create : nodetest/public/stylesheets/style.css
	   create : nodetest/routes
	   create : nodetest/routes/index.js
	   create : nodetest/views
	   create : nodetest/views/layout.jade
	   create : nodetest/views/index.jade
 
	   dont forget to install dependencies:
	   $ cd nodetest && npm install
 
	:node_server zikercn$

运行程序看看

	$ cd nodetest
	$ npm install
	$ node app.js
	Express server listening on port 3000 in development mode

安装成功，浏览器输入`http://127.0.0.1:3000`,即可看到效果。

npm中有许多我们需要的库，比如：

	$ npm install jquery
	$ npm install yui
 