---
layout: posts
title: Mac+Github+Hexo+Next搭建个人博客
date: 2019-04-07 17:16:00
tags:
---

## 前言

一直都有写文章的习惯，不管是收集资料还是发表个人见解，最开始把文章都放在有道笔记，但有道笔记有个不好的点就是不便分享，后来搭建了GitBook，但里面界面不太美观。后来接触到了GitHub-Pages+Hexo，不需要服务器，而且免费。

### 为什么要用Hexo?

Hexo是一个快速、简洁且高效的博客框架，可以在极短时间一键生成所有的静态页面，支持 Markdown，丰富的插件，一键部署到GitHub Pages, Heroku 或其他网站。

## 搭建环境准备
### Node安装

Node.js是国外的网站，下载的服务可能不太友好，可以去国内的Nodejs中文官网下载，选择适合自己的版本安装就好了，安装过程只需要下一步下一步。网址：http://nodejs.cn/download/

![avatar](<http://ppl5t3mrt.bkt.clouddn.com/image/owen/blog/WX20190407-182542@2x.png>)

检查安装是否成功

	node -v 
	npm -v

![avatar](<http://ppl5t3mrt.bkt.clouddn.com/image/owen/blog/WechatIMG342.png>)

### Git安装

Git是一个版本控制工具，主要是在Hexo发布起作用。将本地的Hexo博客（静态文件）同步至Github上。

网址：<https://git-scm.com/downloads>

![avatar](<http://ppl5t3mrt.bkt.clouddn.com/image/owen/blog/20190206115834.png>)

检验是否安装成功：

	git —version

![avatar](<http://ppl5t3mrt.bkt.clouddn.com/image/owen/blog/WX20190407-183330@2x.png>)

## 博客本地安装

### 安装hexo
通过npm来安装hexo
	
	npm install -g hexo-cli

创建网站
	
	hexo init <folder>
	cd <folder>

例如：

	hexo init blog
	cd blog

![avatar](<http://ppl5t3mrt.bkt.clouddn.com/image/owen/blog/WX20190407-184013@2x.png>)

### 网站目录介绍
![avatar](<http://ppl5t3mrt.bkt.clouddn.com/image/owen/blog/WX20190407-184208@2x.png>)

config.yml：博客的配置文件，博客的名称、关键词、作者、语言、博客主题…设置都在里面。

package-lock.json：应用程序信息，插件相关，不用关注。

scaffolds：（中文：脚手架）功能：（配置目标样式）新添加博客文章（posts.md）、新添加博客页（page.md）、新添加草稿（draft.md）

source：source是放置我们博客内容的地方，里面初始只有两个文件夹，一个是drafts（草稿），一个posts（文章），但之后我们通过命令新建tags（标签）还有categories（分类）页后，这里会相应地增加文件夹。

themes：放置主题的目录.


### Hexo命令

Hexo有详尽的中文文档，网址：https://hexo.io/zh-cn/docs/
主要的命令如下：

init 新建网站

	hexo init <folder>

new 新建文章或页面

	hexo new <layout> "title"
	
	layout可选参数（默认posts）：posts：文章、page：页面

g (generate)生成静态页面

	hexo generate
	hexo g //简写

d 将内容部署到配置的服务器
	
	hexo deploy
	hexo d //简写

publish 发布内容（从drafts（草稿）文件夹移到posts（文章）文件夹）
	
	hexo publish <layout> <filename>

server 启动服务 默认访问：http://localhost:4000

	hexo server
	hexo s //简写

根据我的经验，除了第一次部署的时候需要用到hexo init 这个命令外，平时写博客最常用的：

	hexo n 新建文章
	hexo s 启动服务
	hexo g 生成静态页面
	hexo d 发布


### 网站本地效果

执行命令：hexo s
网站本地就启动了，访问http://localhost:4000

![avatar](<http://ppl5t3mrt.bkt.clouddn.com//image/owen/blog/WX20190407-203647@2x.png>)

## 博客Github部署

### 创建存储库

命名必须用账号名，格式保持如下
例如：zhaoouyang316.github.io

![avatar](<http://ppl5t3mrt.bkt.clouddn.com//image/owen/blog/WX20190407-204307@2x.png>)


### 配置SSH-Key

创建ssh-key，是为了执行hexo d部署的时候，可以发布到github

	git config --global user.name youremail
	git config --global user.email youremail@example.com
	ssh-keygen -t rsa -C "youremail@example.com"

![avatar](<http://ppl5t3mrt.bkt.clouddn.com//image/owen/blog/WX20190407-205204@2x.png>)

由于我这里已经生成过了，ssh-keygen后面直接回车即可。
接着拷贝控制台打印的.ssh目录中的id_rsa.pub公钥，将内容复制到GitHub

![avatar](<http://ppl5t3mrt.bkt.clouddn.com//image/owen/blog/WX20190407-205652@2x.png>)

### 同步本地代码至GitHub

执行hexo d 时需要安装一个插件：

	npm install hexo-deployer-git

修改config.yml文件：
	
	type: git
	repo: git@github.com:zhaoouyang316/zhaoouyang316.github.io.git
	branch: master

在命令行中执行：
	
	hexo d

![avatar](<http://ppl5t3mrt.bkt.clouddn.com//image/owen/blog/WX20190407-210336@2x.png>)

此时已经同步代码到GitHub了。

### 打开GitHub-Pages

![avatar](<http://ppl5t3mrt.bkt.clouddn.com//image/owen/blog/WX20190407-210518@2x.png>)

打开 https://zhaoouyang316.github.io/

### 域名解析

- 注册域名
- 进入万网进行域名绑定
- 进入public,新建CNAME
- 把域名写到CNAME里
- 传到github仓库里

![avatar](<http://ppl5t3mrt.bkt.clouddn.com//image/owen/blog/WX20190407-210950@2x.png>)

### 配置主题

![avatar](<http://ppl5t3mrt.bkt.clouddn.com//image/owen/blog/WX20190407-200230@2x.png>)

例如（配置next主题）：

步骤一：下载next项目到themes文件夹

	cd themes
	git clone https://github.com/iissnan/hexo-theme-next themes/next	

步骤二：配置themes插件

	//修改config.yml文件，主题设置为next
	theme: next


添加统一的文章模板参数
把下面的内容加入到 scaffolds/post.md

	cover_img:     # 在文章摘要上显示
	feature_img:   # 在文章详细页面上置顶
	description:   # 文章描述
	keywords:      # 关键字

### valine 评论系统

使用方法请到他的官网查看，并结合下面的配置文件详细添加appID和appKey
https://valine.js.org/