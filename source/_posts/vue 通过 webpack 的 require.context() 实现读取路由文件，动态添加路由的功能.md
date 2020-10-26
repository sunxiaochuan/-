---
title: vue 通过 webpack 的 require.context() 实现读取路由文件，动态添加路由的功能
date: 2020-08-06 15:58:48
tags: [vue-router,vue,技巧,框架,三大框架之一]
categories: [代码/技能进阶]
---

## 前言
  >由于项目中的路由模块越来越多，之前手动 `import` 单个路由文件的方式，显得有些笨重了。
  
  >这里我参照 [Vue.js最佳实践（五招让你成为Vue.js大师）](https://segmentfault.com/a/1190000014085613) 中 “第二招：一劳永逸的组件注册” 的方式，实现了动态增加路由的功能。

<!-- more -->

## 正文

### 源码

1. 目录结构

    > {% asset_img 目录结构.png "目录结构" %}
    
    >可以看到路由文件已经挺多的了，后期可能还会增加

2.  为了方便看到具体代码应该写的位置，源码先截图

    > {% asset_img 源码截图.png "源码截图" %}
    
    >过滤掉的是我这边需要特殊设置的路由文件，具体的业务中可以忽略掉

3.  源码

    ```javascript
    /************************************************************************动态添加路由 */
    // 找到 router 文件夹下以 .js 命名的文件
    const requireRouter = require.context(".", false, /\.js$/);

    requireRouter.keys().forEach(fileName => {
      const routerConfig = requireRouter(fileName);
      // 因为得到的 fileName 格式是: './gridView.js', 所以这里我们去掉头和尾，只保留真正的文件名
      const routerName = fileName.replace(/^\.\//, "").replace(/\.\w+$/, "");

      // console.log(routerName);
      // console.log(routerConfig.default)
      // 动态添加路由
      routerConfig.default && router.addRoutes(routerConfig.default);
    });
    /************************************************************************动态添加路由 */
    ```
