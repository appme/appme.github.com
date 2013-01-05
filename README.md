	zhmme.github.com
	├── _includes/ (存放可复用的模块)
	│   ├──custom/	[自定义模块目录]
	│   ├──JB/		[系统模块目录]
	│   └──themes/ (主要的主题目录)
	│       ├── twitter/	[系统自带的主题]
	│       ├── GreyTexture/	[新主题的模板文件存放目录]
	│       └── zwiki/
	│           ├── default.html
	│           ├── index.html
	│           ├── page.html
	│           ├── post.html
	│           └── settings.yml
	├── _layouts/				[存放当前主题的文件链接文件]
	│   ├── default.html
	│   ├── page.html
	│   └── post.html
	├── _plugins/ (插件存放目录)
	│   └── debug.rb
	├── _posts/ (存放博客正文的地方)
	│   └── 2012-06-28-drupal7.md (.md格式的文章)
	├── _site/ (存放生成静态网站页面的地方)
	├── assets/ (放一些图片,CSS文件或Javascript文件)
	│   └── themes/
	│       ├── twitter/	[系统自带主题的样式目录]
	│       ├── GreyTexture/	[新主题的样式脚本图片目录]
	│           ├── bootstrap/
	│       └── zwiki/
	│           ├── bootstrap/
	│           │   ├── css/
	│           │   │   ├── bootstrap.css
	│           │   │   ├── bootstrap.min.css
	│           │   ├── js/
	│           │   │   ├── bootstrap.js
	│           │   │   ├── bootstrap.min.js
	│           │   └── img/
	│           │       ├── glyphicons-halflings.png
	│           │       └── glyphicons-halflings-white.png
	│           ├── css/
	│           │   └── style.css
	│           └── js/
	│               ├── prettify/
	│               ├── jquery-1.7.2.min.js
	│               ├── vimwiki.js
	│               └── zhm.js
	├──.gitignore	[Git更新排除]
	├──_config.yml	[配置文件]
	├──404.html		[错误页面]
	├──archive.html [存档页]
	├──atom.xml		[RSS文件]
	├──categories.html	[分类页]
	├──changelog.md	[jekyllbootstrap版本更新说明]
	├──CNAME		[域名绑定]
	├──googledb2dfa0762b79223.html	[Google验证文件]
	├──index.md		[首页]
	├──pages.html	[页面页]
	├──Rakefile		[系统文件]
	├──README.md	[项目说明]
	├──robots.txt	[抓取控制]
	├──sitemap.txt	[站点地图]
	├──tags.html	[标签页]

首先要对-[配置文件]_config.yml	-做必要的设置
在仓库目录执行以下命令删除演示目录和文章

	$ rm -rf _posts/core-samples

下面是一个帖子列表的示例

	<ul class="posts">
	  {% for post in site.posts %}
	    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
	  {% endfor %}
	</ul>

网站访问从-[首页]index.md-开始,文件开头包含以下几行

	---
	layout: page	[调用_layouts/page.html模板内容]
	title: 张慧敏	[定义网站标题]
	tagline: ZHM.me	[定义副标题]
	---
	{% include JB/setup %}	[引入_include/JB/setup文件]

跟着来到_layouts/page.html内容如下:

	---
	layout: default	[调用_layouts/default.html内指定的主题]
	---
	{% include JB/setup %}
	{% include themes/GreyTexture/page.html %}	[此处插入_includes/themes/GreyTexture/page.html模板文件]

这个page.html首先layout: default命令加载_layouts/default.html内指定的主题GreyTexture,里面还有{% include themes/zwiki/default.html %}首先加载_includes/themes/GreyTexture/default.html模板文件,开始渲染.结束后在其中的{{ content }}处开始加载_includes/themes/GreyTexture/page.html的内容,接着在这个page.html文件中的{{ content }}处开始加载index.md中{% include JB/setup %}下面的内容.





