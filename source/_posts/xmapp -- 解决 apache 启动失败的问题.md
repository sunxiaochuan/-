---
title: xmapp -- 解决 apache 启动失败的问题
date: 2018-05-16 23:03:04
tags: [xmapp,apache,bug]
categories: [服务器]
---

# 资料

> [参考文章](https://blog.csdn.net/luckchoudog/article/details/71122792) > [xampp 下载页面](http://www.xampp.cc/archives/144)

# 失败的提示截图如下

> {% asset_img 失败的提示截图.png "失败的提示截图" %}

# 解决方法

- 修改 apache 默认的配置，下图我已经将端口号和 ssl 都已经改过了
  > {% asset_img 操作演示1.gif "操作演示1" %}
- 之后如下操作，将两个配置文件里面的配置与上面修改的保持一致，修改之后记得 `ctrl + s` 保存之后再关闭
  > {% asset_img 操作演示2.gif "操作演示2" %}
- 之后测试是否成功
  > {% asset_img 测试结果.png "测试结果" %}

- 再打开浏览器查看 `http://127.0.0.1:8008`
  > {% asset_img 浏览器效果.png "浏览器效果" %}
