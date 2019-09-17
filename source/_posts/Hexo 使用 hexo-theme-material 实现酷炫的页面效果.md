---
title: Hexo 使用 hexo-theme-material 实现酷炫的页面效果
date: 2018-05-09 23:10:31
updated: 2018-05-19 18:12:01
tags: [Hexo,教程,进阶,hexo-theme-material,娱乐]
categories: [软件/包的基础操作]
comments: true
---

# 资料
<!-- 
> [原文地址](https://www.jianshu.com/p/b4cb42d2d48e) -->

> [简单的使用方法参考上篇笔记](http://soulapp.tech/2018/05/09/Hexo%20%E5%BF%AB%E9%80%9F%E3%80%81%E7%AE%80%E6%B4%81%E4%B8%94%E9%AB%98%E6%95%88%E7%9A%84%E5%8D%9A%E5%AE%A2%E6%A1%86%E6%9E%B6/) > [hexo-theme-material Github 地址](https://github.com/viosey/hexo-theme-material)

> [hexo-theme-material 中文文档](https://material.viosey.com/docs/#/) >[hexo-theme-material Icon 图标库](https://material.io/tools/icons/?style=baseline)

# 正文

> 详细的简单的方法这里便不再赘述，可看上面的文档自行操作，这里只记录一下较为复杂的东西，切记要照着上面的顶部文档操作完了之后才可以看下面的操作，不然的话直接操作可能会出错

## 创建页面的步骤，这里以 `about` 页面为例

1.	命令行

	```shell
	hexo new page about
	```

	> 执行上述命令之后在项目的资源目录 `source` 下便有了 `about` 目录，内部还会自动的创建一个 `index.md` 文件可供编辑，结构如下图

	> {% asset_img 目录结构.png "目录结构" %}

2.	之后在 `material` 目录下的 `_config.yml` 配置文件中，设置 `about` 页面的路径即可，具体设置如下
	> {% asset_img 配置文件修改.png "配置文件修改" %}
	> 这里的 `icon` 的值可以去顶部资料资源的 `icon` 图标库中查看
3.	刷新页面进行查看，这里的前提是已启动了服务 `hexo server`
	> {% asset_img 修改后的效果.png "修改后的效果" %}

## 创建新的笔记以及在顶部添加相应的 `tags` 和 `categorise`

1.	命令行

	```shell
	hexo new post testdemo
	```

	>	执行上述命令之后，在项目的 `source -> _posts` 目录下会新建一个 `testdemo.md` 文件，这个就是我们写内容的 `markdown` 文件

2.	下面简单写下示例的文件

	```markdown
	---
	title: 前端的跨域问题
	date: 2018-05-08 22:37:56
	tags: [跨域,web前端,Cookie,jsonp]
	categories: [web前端]
	---
	# 这个是一个测试的页面
	```

3.	之后刷新页面即可，需要注意的是如下所示这些的页面都是需要在 `_config.yml` 文件中相互的对应的设置的
	> {% asset_img 主要的配置.png "主要的配置" %}

# 福利时间到了，技术的目的是为了使这个世界变得更加的美好。

[github 源码](https://github.com/sunxiaochuan/blogapp)

# 更新 2018.5.19

## 增加一个本地搜索的功能

> [文档地址](https://material.viosey.com/docs/#/config_services?id=%E6%9C%AC%E5%9C%B0%E6%90%9C%E7%B4%A2)

1.	使用本地搜索需要安装  [hexo-generator-search](https://github.com/PaicHyperionDev/hexo-generator-search)  插件。

	```shell
	yarn add hexo-generator-search
	```

2.  在站点配置文件 `_config.yml` 中新增如下的代码片段

	```yaml
	# 新增搜索页面  
	search:
		path: search.xml
		field: all
	```
	{% asset_img 外部的配置文件修改.png "外部的配置文件修改" %}
