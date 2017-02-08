---
layout: post
title: "搭建 Octopress 博客"
date: 2017-02-08 15:48:56 +0800
comments: true
categories:
- 工具
---

> Octopress 是基于 Jekyll 的。他们的关系就像 jQuery 与 js 的关系一样。

<!--more-->

第一次接触 Octopress 是在折腾 emacs 学习 org 的时候。

有一篇文章讲的就是使用 org 编写博客，不过 org 相比于 md 非常适合用来做笔记和 TODOs，但是做为博客文章的载体就不合适了，到现在使用的都是 md 来写博客。

这里面的搭建方法，都是从 [Octopress 官网](http://octopress.org/) 看来的。

## 安装 Octopress

首先，获取 Octopress。

	git clone git://github.com/imathis/octopress.git octopress

然后进行安装。

	cd octopress

	gem install bundler
	// 其中 bundler 的安装可能需要权限
	// sudo gem install bundler

	bundle install

安装默认主题。

	rake install

## 预览页面

安装完成后就可以预览页面。

	rake generate
	rake preview

预览使用的默认端口是 4000。

## 部署博客

博客可以部署在 github，也可以部署在自己的服务器上。

如果，部署到 github 上，首先要了解一些 github pages，并申请。之后运行：

	rake setup_github_pages

按照要求输入仓库地址后，项目根目录下会创建一个 _deploy，这里会存放要 push 到 github 的静态网页文件。

	// 生成静态网页
	rate generate
	// 将静态网页存放到 _depoly，并 push 到 github
	rake deploy

如果要部署到自己的服务器，首先要修改 Rakefile。rake 使用 rsync 进行同步，rsync 是一个很有用的工具，有兴趣可以看看。

	## -- Rsync Deploy config -- ##
	# Be sure your public key is listed in your server's 	~/.ssh/authorized_keys file
	ssh_user       = "hxhgta@139.199.22.22"
	ssh_port       = "22"
	document_root  = "~/hxhgta.com/"
	rsync_delete   = false
	rsync_args     = ""  # Any extra arguments to pass to rsync
	deploy_default = "rsync"

这里使用的是 ssh 远程连接（服务器可能要安装 ssh），将 ssh_user 改为 "用户名@服务器 ip"，document_root 改为你存放博客网页的路径。

这样就可以使用

	rake deploy

进行部署了。

## 更换主题

博客的框架是自己选用的主题。

github 上有许多 [第三方主题](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes) 可供选择。

个人觉得比较好看的是:

* MediumFox
* cleanpress
* fabric
* greyshade
* octostrap3
* readify
* villainy
* darkstripes
* foxslide
* octoflat
* oscailte
* slash
* whitespace

下载的主题都放在 .themes 文件夹下。

选好后，执行以下代码。

	cd octopress
	git clone 主题的 github 地址 .themes/主题名
	rake install['主题名']
	rake generate

主题就运用到博客中了。

主题安装后，项目根目录下的 sass、source 两个文件夹，包含主题使用的样式和网页结构，可以自己修改。

再之后，喜欢折腾的同学只要折腾这两个文件夹就够了。

## 写博文

我之前使用的是 org 写博客的内容，现在使用 md 了。不过，想用 org 写博客，可以看 [子龙山人的博客](https://zilongshanren.com/blog/2015-07-19-add-org-mode-support.html?utm_source=tuicool)。

生成博文：

	rake new_post["title"]

就会在 source/_posts 文件夹下生成 md 文件，默认是生成 md 文件的，但是可以在 Rakefile 进行更改。

博文编写完毕，运行

	rate generate
	rake deploy

就生成网页了。

不过，关于写博文，有两点要说：

1. 生成 md 文件后会在文件顶部有博文的配置，这些配置都很易懂。

		---
		layout: post
		title: "title"
		date: 2016-02-08 15:48:56 +0800
		comments: true
		sharing: true
		published: true
		categories:
		- 类别1
		- 类别2
		- ...
		---

2. 博客在目录显示博文时，会将博文全部显示出来。为了避免这种情况，在博文中使用：

		<!--more-->

	将该标记下的内容隐藏，只有打开文章才会显示。同样标记以上的内容还是会显示在目录中。

## 配置

由于 Octopress 是基于 [Jekyll](http://jekyll.com.cn/) 的，要配置使用 Octopress 最好要弄懂 Jekyll。

除此之外，项目目录下的 _config.yml 包含一些个人信息配置，具体看 [官网配置](http://octopress.org/docs/configuring/)。

而 Rakefile 定义了如何将 octopress 跟 Jekyll 连接起来，rake 打包了一些常见的如发布博客主题、生成博客数据、发布博客等一系列命令来简化博主的操作。

## 插件

可以为博客添加插件，增加更多功能。

我使用了多说、百度分享这两个插件，作为评论和分享的插件。除此之外还有许多插件，如 github 插件、微博插件等，可以自己甄选。
   
<br/>       
