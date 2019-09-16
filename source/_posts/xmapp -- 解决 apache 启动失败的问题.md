---
title: xmapp -- 解决 apache 启动失败的问题
date: 2018-05-16 23:03:04
tags: [xmapp,apache,bug]
categories: [服务器]
---

# 资料

> [参考文章](https://blog.csdn.net/luckchoudog/article/details/71122792) > [xampp 下载页面](http://www.xampp.cc/archives/144)

## 失败的提示截图如下

> ![image.png](https://upload-images.jianshu.io/upload_images/9064013-c670dc8e88d7d1be.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 解决方法

1.  修改 apache 默认的配置，下图我已经将端口号和 ssl 都已经改过了
    > ![Animation41.gif](https://upload-images.jianshu.io/upload_images/9064013-d2dfd52e67a282c0.gif?imageMogr2/auto-orient/strip)
2.  之后如下操作，将两个配置文件里面的配置与上面修改的保持一致，修改之后记得 `ctrl + s` 保存之后再关闭
    > ![Animation42.gif](https://upload-images.jianshu.io/upload_images/9064013-b0c2c1b4c4b8df0d.gif?imageMogr2/auto-orient/strip)
3.  之后测试是否成功
    > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-253a6eefbc1e3ed4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 再打开浏览器查看 `http://127.0.0.1:8008`
  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-0eedb458b7e684ff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
