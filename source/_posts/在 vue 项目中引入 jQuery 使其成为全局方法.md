---
title: 在 vue 项目中引入 jQuery 使其成为全局方法
date: 2018-05-10 15:36:33
tags: [vue-cli,jquery,技巧,框架,三大框架之一]
categories: [代码/技能进阶]
---

## 引入 jquery

* 安装

```
npm install jquery --save
```

* 配置

  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-bda0fe1d615d066a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-c6610e7d98d022b9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

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
  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-6fd32a4cc2e690dc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
