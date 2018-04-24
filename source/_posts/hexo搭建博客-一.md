---
title: hexo搭建博客(一)
date: 2018-04-11 11:38:15
tags:
---


## 一、前言

任务第三方文档都没有[官方文档](https://hexo.io/zh-cn/docs/index.html)详细，这里只是记录自身(windows系统)搭建过程中遇到的问题，精简版本，仅做参考。



## 二、安装前提

* node.js
* git

<!--more-->

## 三、安装

### 1. `npm`安装`hexo`

	$ npm install -g hexo-cli

### 2. 初始化，选中一个文件夹作为`blog`站的初始目录，并执行以下命令

	$ hexo init <folder>
	$ cd <folder>
	$ npm install

### 3. 文件、文件夹作用

* node_modules：node插件目录
* scaffolds：模版文件夹
* source：通过命令新建的文档都存放在此
* themes：主题目录
* _config.yml：网站的 [配置](https://hexo.io/zh-cn/docs/configuration.html) 信息，大部分个性化都在此
* package.json：应用程序的信息


### 4. 常用命令

* init：`hexo init [folder]` 新建一个网站
* new：`hexo new [layout] <title>` 新建一篇文章
* server：`hexo server` 启动服务器

> **新建完文章后，启动服务器，会自动把markdown文档转换成html，不需要额外操作**



## 四、个性设置

### 1. 更换主题(NexT)

1) 下载主题：

	$ cd your-hexo-site
	$ git clone https://github.com/iissnan/hexo-theme-next themes/next

2) 修改`_config.yml`配置：找到 theme 字段，并将其值更改为 next

3) 更换NexT主题外观：修改主题的`_config.yml`配置，搜索`scheme`

### 2. 更换默认语言

1）语言配置在主题中，先在`themes\landscape\languages`找到对应语言设置

2）修改根`_config.yml`配置，搜索`language`，修改为`zh-Hans`

### 3. 更换`menu`项

修改主题的`_config.yml`配置，搜索`menu`，放开或注释即可

### 4. 开启本地搜索

1）修改主题的`_config.yml`配置，搜索`local_search`，下面的`enable`改为`true`

2）站点的根目录下执行以下命令：npm install hexo-generator-search --save

3）站点的根目录下执行以下命令：npm install hexo-generator-searchdb --save

### 5. 关闭动画
	
修改主题的`_config.yml`配置，搜索`motion`，下面的`enable`改为`false`

### 6. 主页文章添加阴影效果

{% asset_img shadow.png %}

打开\themes\next\source\css\_custom\custom.styl,向里面加入：

	// 主页文章添加阴影效果
	.post {
	   margin-top: 60px;
	   margin-bottom: 60px;
	   padding: 25px;
	   -webkit-box-shadow: 0 0 5px rgba(202, 203, 203, .5);
	   -moz-box-shadow: 0 0 5px rgba(202, 203, 204, .5);
	}

### 7. 支持图片

1）修改主题的`_config.yml`配置，搜索`post_asset_folder`，改为`true`

2）在对应文章目录下新增一个和文章名称一样的目录，存放图片(使用命令`hexo new`新建文章会默认创建此目录)

3）在文章中使用`{% asset_img test.png %}`引入图片，[参考文章传送门1](https://www.jianshu.com/p/c2ba9533088a)、[参考文章传送门2](https://hexo.io/zh-cn/docs/tag-plugins.html)

### 8. 实现统计功能

{% asset_img wordcount.png %}


1）站点的根目录下执行以下命令：npm install hexo-wordcount --save

2）NexT主题已经支持字数统计，其他主题需要在主题的`_config.yml`配置，增加以下

	# Post wordcount display settings
	# Dependencies: https://github.com/willin/hexo-wordcount
	post_wordcount:
	  item_text: true
	  wordcount: true
	  min2read: true

3）修改`{blog}\themes\next\layout\_macro\post.swig`

	<span title="{{ __('post.wordcount') }}">
	     {{ wordcount(post.content) }} 字
	</span>

	<span title="{{ __('post.min2read') }}">
	   {{ min2read(post.content) }} 分钟
	</span>


### 9. 标签

1）站点的根目录下执行以下命令：hexo new page tags

2）打开 tags/index.md ，并改成：

	title: 标签
	date: 日期
	type: "tags"
	comments: false

### 10. 分类

1）站点的根目录下执行以下命令：hexo new page categories

2）打开 category/index.md ，并改成：

	title: 分类
	date: 日期
	type: "categories"
	comments: false

## 五、其他

1. 推荐使用`<!--more-->`进行首页展示隔断

2. [更多个性设置](https://blog.csdn.net/qq_33699981/article/details/72716951)



## 六、插件推荐

1. 后端管理插件：[hexo-admin](http://yeshaoting.cn/article/hexo/hexo%E4%BD%BF%E7%94%A8%E8%BF%9B%E9%98%B6/)