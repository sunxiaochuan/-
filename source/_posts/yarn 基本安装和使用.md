---
title: yarn 基本安装和使用
date: 2018-05-14 12:57:03
updated: 2018-05-21 15:23:26
tags: [yarn,安装工具,教程]
categories: [软件/包的基础操作]
---

# 资料

> [yarn 中文网](https://yarn.bootcss.com/)

> [yarn 中文网 安装](https://yarn.bootcss.com/docs/install.html)

> [yarn 中文网 用法](https://yarn.bootcss.com/docs/usage.html)

> [yarn 与 npm 的命令行小结](http://www.jb51.net/article/95199.htm)

<!-- more -->


# 安装

* 前提
  > 如果你使用安装程序的方式，你需要首先安装  [Node.js](https://nodejs.org/)
* 这里我使用的是 npm 的安装方式

```shell
npm install -g yarn
```

* 查看是否安装成功

```shell
yarn -v
```

# 使用

* 常用命令

```shell
# 初始化一个项目
yarn init
# 装包
yarn add packagename
# 更新包
yarn upgrade packagename
# 删除包
yarn remove packagename
# 安装所有包
yarn
yarn install
# 发布包
yarn publish
# 查看包的缓存列表
yarn cache list
# 全局安装包 == npm -g
yarn global
```
