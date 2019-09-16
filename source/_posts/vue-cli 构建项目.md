---
title: vue-cli 构建项目
date: 2018-05-10 15:07:18
tags: [vue-cli,vue,技巧,框架,三大框架之一]
categories: [代码/技能进阶]
---

## vue-cli 构建项目

> [官网地址](https://cn.vuejs.org/v2/guide/installation.html#%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%B7%A5%E5%85%B7-CLI)

* 命令行
  ```base
  # 全局安装 vue-cli
  $ npm install --global vue-cli
  # 创建一个基于 webpack 模板的新项目
  $ vue init webpack your-project-name
  # 安装依赖，走你
  $ npm install
  # 进入项目
  $ cd your-project-name
  # 开发版本打包并运行
  $ npm run dev
  # 线上环境整个项目打包  生成 dist 可以直接部署到服务器上的文件夹
  npm run build
  ```
