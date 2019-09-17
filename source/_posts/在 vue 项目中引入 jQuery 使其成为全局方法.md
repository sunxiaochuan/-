---
title: 在 vue 项目中引入 jQuery 使其成为全局方法
date: 2018-05-10 15:36:33
tags: [vue-cli,jquery,技巧,框架,三大框架之一]
categories: [代码/技能进阶]
---

## 引入 jquery

* 安装

  ```shell
  npm install jquery --save
  ```

* 配置
  > {% asset_img 配置1.png "配置1" %}
  > {% asset_img 配置2.png "配置2" %}

  ```javascript
  // 先在顶部引入 webpack
  const webpack  = require('webpack')

  // plugins 中添加
  new webpack.ProvidePlugin({
      'window.jQuery': 'jquery', // 为了兼容其他的插件
      jQuery: 'jquery',
      $: 'jquery'
      })
  ```

* 使用
  > {% asset_img 使用.png "使用" %}
