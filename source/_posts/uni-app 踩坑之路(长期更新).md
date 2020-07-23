---
title: uni-app 踩坑之路(长期更新)
date: 2020-07-21 17:37:05
tags: [uni-app,踩坑之路]
categories: [软件/包的基础操作]
---
## 资料
>[`uni-app` 官网](https://uniapp.dcloud.net.cn/)

## 正文

<!-- more -->

### 1.  基本创建并启动工程操作
>[原文地址](https://uniapp.dcloud.net.cn/quickstart?id=_2-%e9%80%9a%e8%bf%87vue-cli%e5%91%bd%e4%bb%a4%e8%a1%8c)
-  项目的创建
    ```shell
    # 全局安装脚手架的两种方式
    npm install -g @vue/cli
    # OR
    yarn global add @vue/cli

    # 新建工程 => 选择`默认模板`即可
    vue create -p dcloudio/uni-preset-vue my-project
    ```
-  项目的启动（本地启动微信小程序服务）
    ```shell
    # 本地启动微信小程序服务
    yarn dev:mp-weixin
    ```
-  之后手动在微信开发者工具中导入该项目，一次选中 `my-project => dist => dev => mp-weixin` 目录点击确定即可

### 2.  安装 `sass-loader` 之后，由于版本过高，导致报错无法成功编译
-  为了使用 `sass` 安装相应需要的依赖
    ```shell
    yarn add node-sass sass-loader -D
    ```
-  由于我安装的 `sass-loader` 是 `9.0.2` 版本的，导致无法正常编译，报错信息 `options has an unknown property 'prependData'. These properties are valid:`，解决方法修改版本号 `9.0.2 => 8.0.2`，重新安装依赖
    >[该问题参考文章："【已解决】uniapp项目,通过cli指令新建的项目,在任意页面style标签使用lang="scss"报错:options has an unknown property 'prependData'"](https://ask.dcloud.net.cn/question/101104)



### 3.  微信小程序底部的 `icon` 

1.   `icon` 尺寸需要是 `81*81` 的，不然会非常模糊尺寸需要是 `81*81` 的，不然会非常模糊
        >[参考文章：小程序底部的tabbar图片显示老是会模糊，不管放多大的图都模糊，什么原因](https://segmentfault.com/q/1010000009630810/a-1020000009630903)
        -  对比图
        {% asset_img 对比图.png "对比图" %}

2.   `icon` 的周围要适当的留白，不能全部填满，不然不好看
        -  示意图，如下所示对比非常的明显
        {% asset_img 示意图.png "示意图" %}