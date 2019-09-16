---
title: 修改 hosts 文件实现快速访问站点的需求
date: 2018-05-16 14:41:43
tags: [hosts,教程]
categories: [软件/包的基础操作]
---

# 正文

* 这个示例实际是为了解决内网访问不了改域名的问题

#### 使本机可以通过相应的域名访问到相应的站点；下面是详细的操作步骤

* 在本机找到 `hosts` 文件

  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-ef057a0d37f0e23f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 将其拖拽至代码编辑器中进行编辑

  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-6ac483af417d32c3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 如上图：重点是最后一行，写法如下

```
ip地址     域名
```

* 在浏览器中测试结果
  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-f7674184da00866b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
