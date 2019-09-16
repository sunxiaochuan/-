---
title: 使用 nginx 配置多个站点
date: 2018-05-16 14:34:17
tags: [nginx,linux,centos,站点,部署,教程]
categories: [服务器]
---

# 准备工作

* 一台服务器(我的是阿里云的 `centos` 系统，亦可以使用虚拟机)
* 服务器上必须已安装 `nginx`(我的版本是 1.12.2，版本不同可能会存在一些小差异)
* 服务器还需安装 unzip 包

# 前言

* 我的本机是 `windows` 系统，使用的是 `Xshell` 软件登录 远程服务器
* 本机安装的是 `cmder` 软件，使得可以在本机使用 `shell` 命令行

# 开始操作

> 我的笔记：[Linux 命令行操作（持续更新）](https://www.jianshu.com/p/64a7ab15358c)
> 本文操作：[参考他人文章](https://blog.csdn.net/marksinoberg/article/details/77816991)

1.  首先是站点目录的相关一系列操作

* 进入服务器创建一个存放站点文件夹的目录

```shell
mkdir /home/www
cd www
ls
# 创建一个站点目录
mkdir blog
cd blog
pwd
cd ..
# 创建另一个站点目录
mkdir  fxjiacheng
cd fxjiacheng
pwd
```

* 将本地桌面的两个站点压缩包通过 `scp` 命令，上传至该目录下，下面的命令是在本机命令行编辑的
  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-6b4eb5d23d90e168.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```shell
scp public.zip dis root@yourserverip:/home/www/blog
enter yourserverpassword

scp dist.zip dis root@yourserverip:/home/www/fxjiacheng
enter yourserverpassword
```

* 两个站点压缩包上传成功之后，在服务器中进行查看，并解压

```shell
cd /home/www
ls
cd blog
ls
# 创建一个 html  目录存放文件
mkdir html
cd html
cd ..
# 将压缩包复制至 html 目录下进行解压
cp public.zip html
cd html
unzip public.zip


# 另一个站点目录操作与上面大致相同
cd ../..
ls
cd fxjiacheng
ls
# 创建一个 html  目录存放文件
mkdir html
cd html
cd ..
# 将压缩包复制至 html 目录下进行解压
cp dist.zip html
cd html
unzip dist.zip
```

2.  之后是重头戏，进入 `nginx` 配置目录，写相应的配置文件

```shell
cd /etc/nginx
ls
# 查看 nginx 默认的配置文件
cat nginx.config
```

> ![image.png](https://upload-images.jianshu.io/upload_images/9064013-869edfa5a59fcd56.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 上图可以看到 `nginx` 默认配置的一个目录，这里我选择将配置文件写在这个目录下

```shell
cd /etc/nginx/sites-enabled
```

* 新建并编辑一个站点的配置文件 ，这里需要注意的一点是：配置文件的后缀名必须是 `.config` 这样才能与默认的配置里面相呼应

```shell
vi sites_blog.conf
```

* 内容编辑如下
  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-171fc9c47dccb7eb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 以上面同样的方法新建另一个站点配置文件

```shell
vi sites_fxjiacheng.conf
```

* 内容编辑如下
  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-0441d18af8b436d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.  完成上面的两个之后可别忘了要重新加载 `nginx` 的 配置文件噢（这个东西不知何故我总是会忘~~）

```shell
#  下面的两个命令都可以
systemctl  restart  nginx
nginx -s reload
# 查看 nginx 状态
systemctl  status nginx
```

4.  之后就是测试是否成功了

* 浏览器输入你的服务器 IP + 端口号(6666)
  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-f170adcfbd0afa83.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 浏览器输入你的服务器 IP + 端口号(8888)
  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-7cf4c244e472c3e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 细心的同学可能发现了，我用了两个不同的浏览器，原因是：6666 这个端口不知何故在谷歌浏览器中总是访问失败~~
  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-d6a74ac9f33bf275.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 更新： 6666 端口问题，我在配置文件中把端口改为 9999 就可以了，推断是端口被某个程序占用所致
  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-c9a50434da4bebd8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
