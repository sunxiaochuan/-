---
title: vue-router 修改 mode 为 history
date: 2018-05-10 15:28:58
tags: [vue-cli,vue-router,技巧,框架,三大框架之一]
categories: [代码/技能进阶]
---

- 在 router 下的路由文件里设置格式，将页面上路由中默认显示的 `#/` 给去掉

  ```javascript
    // 去掉路由中自带的 #/ 这种东西
    mode: 'history',
  ```

  > {% asset_img 修改的代码.png "修改的代码" %}

- 需要注意的是使用了 `history` 之后需要在服务器部署时增加一些配置，具体方法插件下面官方写的配置方法
  > [配置方法](https://router.vuejs.org/zh-cn/essentials/history-mode.html)
