---
title: Hexo 主题新增评论和阅读量的功能
date: 2020-05-22 14:05:36
tags: [Hexo,教程,进阶,hexo-theme-material,娱乐]
categories: [软件/包的基础操作]
---

# 资料

>[Valine 一个静态网站的评论系统，不需要后端，数据储存在 LeanCloud。](https://valine.js.org/)

>[新增阅读量功能参考文章：Hexo搭建博客系列：（五）Hexo添加不蒜子和LeanCloud统计无标题文章](https://www.jianshu.com/p/702a7aec4d00)

# 准备工作

>由于评论和阅读量的功能都需要依托于 [LeanCloud](https://www.leancloud.cn/) 平台，所以需要去该平台官网注册一个可用的账号，具体的注册流程这里便不再概述，只是有一点，注册成功之后创建应用之前还需要“实名认证”，他们这边采取的是支付宝扫码认证的策略。

<!-- more -->

# 正文

## 增加评论功能

1.  准备工作完成之后，登录上 [LeanCloud](https://www.leancloud.cn/)  