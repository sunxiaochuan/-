---
title: VS Code 编辑器 Vetur 扩展更新至 0.31.0 版本，无法使用的问题记录
date: 2020-12-09 14:59:25
tags: [VS Code,Vetur]
categories: [软件/包的基础操作]
---

## 问题截图

<!-- more -->

-  由于扩展之前都是默认的自动更新，所以直接就弹出了下图所示的警告语
    
    {% asset_img 警告语.webp "警告语" %}

-  重点是整个项目中的 `.vue` 文件都无法格式化了，对于有强迫症的我而言，基本就是没法干活儿了 /摊手

    {% asset_img 无法格式化.webp "无法格式化" %}


## 问题解决
-  首先自己百度了一会儿，无果。之后选择去 `github` 参观一下。还好看到了一个相似的问题 [Add command create vetur.config.js file #2537](https://github.com/vuejs/vetur/issues/2537)
    >经过查看下面官方作者的解答，我这边试了一下，果然好用了。

    {% asset_img 官方解答.webp "官方解答" %}

-  但是好使了一个多小时之后，又出现了第一个图中的警告语，然后我似乎也明白了，尝试格式化一下，果然又不好使了。

-  最后就是——重启大法！好在扩展可以自行选择使用的版本，下载完重新加载，bingo！

    {% asset_img 重启大法1.webp "重启大法1" %}
    {% asset_img 重启大法2.webp "重启大法2" %}
    {% asset_img 重启大法3.webp "重启大法3" %}
