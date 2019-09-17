---
title: Nginx中让url支持中文URL与中文目录路径
date: 2018-05-17 22:46:07
tags: [nginx,服务器,部署]
categories: [服务器]
---
# 资料

> [原文地址](https://yq.aliyun.com/ziliao/29288)

# 操作

* 先确定你的系统是 UTF 编码 (我这边是阿里云 centos 服务器)

  ```shell
  env|grep LANG
  # 输出结果
  # LANG=en_US.UTF-8
  ```

* 之后修改 `/etc/profile` 文件

  ```shell
  vi /etc/profile
  i

  # 添加下面的两行代码
  export zh_CN.utf-8
  export LANG=zh_CN.utf-8
  ```

  > {% asset_img 修改配置.png "修改配置" %}

* 之后登录阿里云网站重启服务器
* 在执行命令行，查看服务器端字符集

  ```shell
  locale
  ```

  > {% asset_img 查看配置.png "查看配置" %}

* 修改 nginx 的配置文件中的编码格式
  > {% asset_img 修改nginx配置.png "修改nginx配置" %}
