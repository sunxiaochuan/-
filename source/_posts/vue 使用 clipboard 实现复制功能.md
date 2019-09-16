---
title: vue 使用 clipboard 实现复制功能
date: 2018-05-10 15:49:16
tags: [vue-cli,vue,插件,框架,三大框架之一]
categories: [代码/技能进阶]
---

## vue 使用 clipboard 实现复制功能

> [原文地址](https://blog.csdn.net/guxuehua/article/details/79169190)

* 安装依赖 clipboard.js

  ```
  npm install clipboard --save
  ```

* 在需要使用的地方 require 引用

  ```
  var clipboard = require('clipboard');
  ```

* 在页面加载后调用该方法即可
  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-f3d7d4e56d786d10.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
