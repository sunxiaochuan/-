---
title: vue-cli 项目模板中使用 less 方法
date: 2018-05-10 15:20:09
tags: [vue-cli,vue,技巧,框架,三大框架之一,less]
categories: [代码/技能进阶]
---

# 项目模板中使用 less 方法

> [原文地址](https://www.aaa1a.xyz/movie/guochanzipai/bc1c9e69d117b5c3be822ca22b137f08.html)
> vue-cli 构建的项目默认是不支持 less 的，需要自己添加。

- 首先安装 less 和 less-loader ，在项目目录下运行如下命令

  ```shell
  # npm安装
  npm install less less-loader --save-dev
  # 或者使用 yarn
  yarn add less less-loader --dev
  ```

- 安装成功后，打开 `build/webpack.base.conf.js` ，在 `module.exports = `对象的 `module.rules` 后面添加一段：

  ```shell
  module.exports = {
      //  此处省略无数行，已有的的其他的内容
      module: {
          rules: [
            //  此处省略无数行，已有的的其他的规则
            {
              test: /\.less$/,
              loader: "style-loader!css-loader!less-loader",
            }
          ]
      }
  }
  ```
  > {% asset_img 使用示例1.png "使用示例1" %}

- 最后在 `.vue` 页面代码中的 style 标签中 加上 lang="less" 属性即可

  ```vue
  <style scoped lang="less">

  </style>
  ```
  > {% asset_img 使用示例2.png "使用示例2" %}

- 之后在项目中测试是否成功

  ```shell
  npm install less less-loader --save-dev
  npm run dev
  ```
  > {% asset_img 命令行编译结果.png "命令行编译结果" %}

- 在浏览其中打开相应页面，这个页面是 `/` 根页面点击跳转过来的子路由
  > {% asset_img 测试效果1.png "测试效果1" %}
  > {% asset_img 测试效果2.png "测试效果2" %}
  > 可以看到样式编译成功了 哦耶~
