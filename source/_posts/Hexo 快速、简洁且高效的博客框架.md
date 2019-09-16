---
title: Hexo 快速、简洁且高效的博客框架
date: 2018-05-09 10:07:56
tags: [Hexo,教程,娱乐]
categories: [软件/包的基础操作]
---

# 资料
>[中文官网地址](https://hexo.io/zh-cn/)
[详细的文档](https://hexo.io/zh-cn/docs/) 更多的骚操可以前去查看文档
# 快捷使用命令行创建一个项目
```
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```
# 问题修复
## 1. jQuery 引入失败
-  问题截图
    >{% asset_img jQuery引用失败问题截图.png "jQuery引用失败问题截图" %}
-  产生的原因
    >无法获取到这个 cdn 上的资源
-  解决方法
    >替换 cdn 这里我使用的是 [bootcdn.cn 上的资源地址](http://www.bootcdn.cn/jquery/)
    {% asset_img 替换jQuery地址方法.png "替换jQuery地址方法" %}

-  之后刷新一下页面即可
    >{% asset_img 成功展示.png "成功展示" %}
## 2. 引用内部静态图片资源的方法
>[官网文档](https://hexo.io/zh-cn/docs/asset-folders)
-  首先在 `_config.yml` 文件中开启 `post_asset_folder: true` 配置
-  之后在命令行中新建文章
    ```shell
    # 新建文章， layout 非必填项，为空的话默认使用的是 post 布局
    hexo new layout page-title
    ```
-  然后可以在 `source -> _posts` 目录下可以看到上面命令行所新建的对应的 `page-title.md` 文件和 `page-title` 文件夹
    >在 `page-title` 文件夹中放置一个测试的图片文件 `alipay.jpg`，`page-title.md` 文件中引用的方法如下

    ```markdown
    {% asset_img alipay.jpg 测试图片 %}
    ```