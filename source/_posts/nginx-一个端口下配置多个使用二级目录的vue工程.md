---
title: nginx 一个端口下配置多个使用二级目录的vue工程
date: 2019-10-17 16:58:49
tags: [nginx,服务器,部署,vue,二级目录]
categories: [服务器]
---

## 需求
这次的需求是将多个 `vue` 工程集成到一个单独的工程里面使用，用户相关的公用一套，路由也是如此，还要单独加一些新的功能页面进去，简单来说就是将几个工程里的功能合并到一个工程里面，之前每个工程单独的用户登录和路由需要改造（这个之前确实是这样想的）。

<!-- more -->

## 思路
乍一听，这个似乎工程量是很大的，多个工程中的代码一个一个的粘贴复制吗？打扰了~~

很明显这么大的工作量，是很难如期交付上线的，所以我一直在想用没有取巧的方法来实现。

实现的思维拓展过程：
多个工程的目录可不可以保留不变，保持独立开发的状态，然后外面给他们包一个公用的登录框架呢？
这样一来不就大大减少了工作量嘛。
如何才能实现上面的想法呢？
很明显实现这个想法 `nginx` 比较的合适。

## 动手操作

### 前提条件
- 自己的服务器一台，虚拟机也是可以的，只要本机可以正常访问。
- 服务器上安装 `nginx`
- 有两个独立的 `vue` 工程（我的两个工程名字 `test1` 和 `custInfo`，最基本的有点区别的工程就可以了），再加一个单独的 `index.html` 文件（这个文件代表的相当于是上面说的 包一个公用的登录框架 这个东西）

### 重点的操作
#### 1.  修改两个 `vue` 工程中 `vue.config.js` 文件的 `publicPath` 属性，这个改的是 [部署应用包时的基本 URL](https://cli.vuejs.org/zh/config/#publicpath)
```javascript
// test1 项目
publicPath: process.env.NODE_ENV === 'production' ? '/test1/' : '/'

// custInfo 项目
publicPath: process.env.NODE_ENV === 'production' ? '/custInfo/' : '/'
```

#### 2.  修改 `vue` 工程中的 `router -> index.js` 路由文件，在 `new Router()` 对象中新增一个 `base` 属性
```javascript
// test1 项目
base: process.env.NODE_ENV === 'production' ? '/test1/' : '/'

// custInfo 项目
base: process.env.NODE_ENV === 'production' ? '/custInfo/' : '/'
```
{% asset_img 路由文件修改.png "路由文件修改" %}

#### 3.  接着就可以把两个工程各自 `yarn build` 打包了，之后将生成两个文件夹 `test1` 和 `custInfo`，再单独新建一个有点文字内容的静态文件 `index.html`，将这三个东西都上传到服务器上，上传的方法我这里是本地压缩成 `zip` 文件，然后用 `scp` 命令放到服务器上，再在服务器上用 `unzip` 命令解压的

#### 4.  简单描述下我的服务器上相关的基本信息
- 静态文件放置的目录 `/home/test/html`
- 因为服务器上多个端口都放置了些东西，这个 `test` 工程放在了 `8889` 端口上
- 具体的 [使用 nginx 配置多个站点](http://www.soulapp.tech/2018/05/16/%E4%BD%BF%E7%94%A8%20nginx%20%E9%85%8D%E7%BD%AE%E5%A4%9A%E4%B8%AA%E7%AB%99%E7%82%B9/) 的过程这里不再详述了（你也可以不这样操作，只用一个外部公用的配置文件 `nginx.conf`），简单来说就是在 `nginx -> http` 配置里面加了一句 `include /etc/nginx/sites-enabled/*.conf`，然后所有的站点就可以单独在 `/etc/nginx/sites-enabled` 目录下新建一个相应的 `.conf` 文件了
{% asset_img nginx配置include.png "nginx配置include" %}
- 所有的 `.conf` 配置文件只需要写 `server` 对象即可
- 最后看一下目录下的文件
{% asset_img 服务器上的目录文件.png "服务器上的目录文件" %}

#### 5.  接着就是重头戏了，写 `nginx` 配置文件，这里我在 `/etc/nginx/sites-enabled` 目录下新建了一个 `sites_test.conf` 文件，编辑内容如下
```conf
server {
  listen       8889;                      # 监听端口
  server_name  www.test.com test.com;     # 站点域名
  root         /home/test/html;       # 站点根目录
  charset      utf-8;                     # 默认编码设置为utf-8
  index      index.html index.htm;      # 默认导航页

  location / {
      root /home/test/html;
      index index.html;
      try_files $uri $uri/ /index.html;
  }

  location /test1 {
      root /home/test/html/;
      index index.html;
      try_files $uri $uri/ /test1/index.html;
  }

  location /custInfo {
      root /home/test/html/;
      index index.html;
      try_files $uri $uri/ /custInfo/index.html;
  }
}
```
大功告成？别忘了还得重启一下 `nginx` 服务哟~
```
nginx -s reload
```

#### 6.  好了可以测试了
- `index.html` 入口文件测试结果
{% asset_img 入口文件测试结果.png "入口文件测试结果" %}

- `test1` 项目测试结果
{% asset_img test1项目测试结果.png "test1项目测试结果" %}

- `custInfo` 项目测试结果
{% asset_img custInfo项目测试结果.png "custInfo项目测试结果" %}

bingo！当然了，上面的过程都是自己摸索出来的，嗯~ 被网上的几篇小白文坑了下 0.0，当然了后续还得完善 `单点登录` 的功能。
