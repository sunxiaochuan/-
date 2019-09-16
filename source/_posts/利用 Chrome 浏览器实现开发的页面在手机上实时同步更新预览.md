---
title: 利用 Chrome 浏览器实现开发的页面在手机上实时同步更新预览
date: 2018-05-25 15:05:59
tags:
categories:
---


# 资料
>[参考地址](https://mp.weixin.qq.com/s?__biz=MzAxODE2MjM1MA==&mid=2651554224&idx=1&sn=039d86aea6318a365f4e476cd84c6677&chksm=80255671b752df6730726a63fb8d666db62f039d42e2229da49a26d4d80d802dad5a36a0a614&mpshare=1&scene=1&srcid=05252AIMEZbKjqJtUoYXgp4P#rd)

# 准备工作
-  PC 端安装 [谷歌浏览器](https://www.google.cn/intl/zh-CN/chrome/)
-  手机需要开启【开发者模式】->【USB调试】
-  手机数据线
-  项目需在PC端本地起一个服务运行

#  开始操作

## 1.  本地起服务（以 [vue](https://cn.vuejs.org/) 开发为基石的）
-  我这里使用的是 [vue-cli](https://www.jianshu.com/p/e555bc60b96b) 构建的项目，运行方法 `npm run dev`，默认的是 `8080` 端口号，我这边因为开启了多个项目，所以是 `8081` 端口
{% asset_img 服务启动成功.png "服务启动成功" %}
-  上图证明已编译成功

## 2.  在 `Chrome` 浏览器中骚操
-  谷歌浏览器打开 `http://localhost:8081` 地址
{% asset_img 浏览器预览.png "浏览器预览" %}
-  `F12` 打开开发者工具，依次找到 `More tools` -> `Remote devices`(远程设备) -> `setting` -> `port forwarding`(端口转发)，之后点击 【Add Rule】，输入 【8081】端口号 + 手机端需要请求的地址 `localhost:8081`，最后点击【Add】按钮保存，下面为 演示 GIF 图
{% asset_img 演示图.gif "演示图" %}

## 3.  上面的是电脑端操作，下面是手机端操作
-  用数据线将手机和电脑连接，开启手机的【开发者模式】->【USB调试】,多个型号开启方法不尽相同，可自行百度
-  手机端打开浏览器测试
    -  小米手机自带浏览器测试成功   `http://localhost:8081`
    -  `UC` 浏览器测试成功   `http://localhost:8081`
    -  `Chrome` 浏览器测试成功   `localhost:8081`  唯一的方便之处是不需要输入协议前缀了
