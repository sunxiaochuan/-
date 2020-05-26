---
title: 使用 serve 在本地预览生产环境构建的代码
date: 2020-05-26 10:55:41
tags: [serve,本地运行,生产环境,单页,教程]
categories: [软件/包的基础操作]
---

# 引言

>之前一直使用的是 [http-serve](https://www.npmjs.com/package/http-server) 这个 npm 包，来在本地开启服务的，可见之前的文章 [使用 http-server 在本地开启超轻量级web服务器](https://www.jianshu.com/p/497e68db20c1) 虽然可以开启 `https` 的服务，但是有个诟病 "无法将如今主流的单页应用如服务器上使用 `nginx` 那般将所有未找到的请求重写为`index.html`"。
前些天偶然的机会在 [vue-cli 官网推荐的#本地预览方法](https://cli.vuejs.org/zh/guide/deployment.html#%E6%9C%AC%E5%9C%B0%E9%A2%84%E8%A7%88) 看到推荐的这个依赖（印象中之前推荐的好像不是这个，也从侧面看出开源工作者们产出频率还是蛮高的），上手之后觉得这个依赖使用起来也是相当的方便的。

<!-- more -->

# 资料

>[vue-cli 官网推荐的#本地预览方法](https://cli.vuejs.org/zh/guide/deployment.html#%E6%9C%AC%E5%9C%B0%E9%A2%84%E8%A7%88)
[serve github 地址](https://github.com/zeit/serve)
[serve npm 地址](https://www.npmjs.com/package/serve])

# 正文

1.  基本的安装和常用命令
```
# 安装 下面的两种方法任选其一
yarn global add serve
npm install -g serve

# 进入当前项目的目录中使用
serve

#  指定运行某个文件夹
serve folder_name

#  指定运行某个打包的单页项目文件夹
# -s 参数的意思是将其架设在 Single-Page Application 模式下
#  Rewrite all not-found requests to `index.html` 这将所有未找到的请求重写为`index.html`
serve -s folder_name

# 查看当前的版本
serve -v

# 查看帮助指南
serve --help
```
