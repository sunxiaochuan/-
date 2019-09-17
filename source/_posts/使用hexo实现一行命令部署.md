---
title: 使用hexo实现一行命令部署
date: 2019-09-16 16:24:23
tags: [hexo,nginx,部署]
categories: [软件/包的基础操作]
---

# 参考资料
>[使用Nginx+Hexo光速搭建博客并实现服务器自动部署 - 个人文章 - SegmentFault 思否](https://segmentfault.com/a/1190000009723457)

# 前期准备
- `node` 环境(本地和服务器)
- `git` 命令(本地和服务器)
- `nginx` 我这里用的是这个服务器
- [hexo 的入门基本使用方法](https://hexo.io/zh-cn/docs/) 这里就不做简单概述了

# 正文
## 基本操作
>  我这边基本就是照着上面的参考文章走的，基本操作的前提是前期准备已经做好，本地已经使用 hexo 新建了一个项目了
### 1. 服务器配置
- 新建一个 `git` 用户
    ```shell
    adduser git
    ```
- git 仓库初始化
  ```shell
  # 进入新建用户后默认生成的用户文件夹
  cd /home/git

  # 初始化，会创建一个 hexo.git 文件夹
  git init --bare hexo.git

  # 权限修改
  chown -R git:git hexo.git
  ```
- 服务器端配置公钥
    - 首先需要在本地电脑查看一下本地是否已有公钥
        ```shell
        # 查看公钥文件
        cat ~/.ssh/id_rsa.pub
        ```
    - 如果上述文件并没有，需要生成一对密钥文件
        >[生成密钥的教程](https://www.liaoxuefeng.com/wiki/896043488029600/896954117292416) 这里生成之后，还在 github 上进行了配置
    - 密钥生成之后，将公钥复制出来
        ```shell
        # 查看密钥文件，之后手动复制文本
        cat ~/.ssh/id_rsa.pub
        ```
    - 之后开始操作服务器端，首先在 `/home/git` 目录下新建一个 `.ssh` 文件夹，再添加一个存储公钥的文件 `authorized_keys`

        ```shell
        mkdir .ssh
        cd .ssh
        vim authorized_keys
        ```
    - 在 `vim` 编辑文件的窗口中，将之前复制的公钥内容粘贴其中
        ```shell
        # vim 基本操作命令
        
        # 进入编辑状态
        i
        # 退出编辑状态(编辑完成之后)，键盘右上角
        ESC
        # 进入执行命令状态
        :
        # 保存并退出
        wq
        Enter
        # 取消并退出
        q!
        Enter
        ```
- 服务器配置 nginx
    - 修改默认的配置文件
        ```shell
        vim /etc/nginx/nginx.conf
        ```
    - 主要是修改 `http -> server -> root` 的配置
    	>{% asset_img nginx配置示例.png "nginx配置示例" %}
    - 之后需要重启 `nginx` 服务，切记：每次修改配置文件，服务都要手动重启一下
        ```shell
        nginx -s reload
        ```
- 新建一个可以自动迁出 `git` 项目的 `shell` 脚本文件 `post-update`
    - 进入 `/home/git/hexo.git/hooks` 目录
        ```shell
        cd /home/git/hexo.git/hooks
        ```
    - 复制文件 `post-update.sample`，粘贴的新文件名称为 `post-update`
        ```shell
        cp post-update.sample post-update
        ```
    - `vim` 编辑 `post-update` 文件，将文件的原内容删除，换成下面的
        ```shell
        #!/bin/sh
        git --work-tree=/home/git --git-dir=/home/git/hexo.git checkout -f
        ```
    - 修改权限使其可执行
        ```shell
        chmod +x post-update
        ```

### 2. 本地配置
- 找到本地项目中的 `_config.yml` 配置文件，修改 `deploy` 属性
    ```yml
    deploy:
      type: git
      repo: git@server:/home/git/hexo.git
      branch: master
    ```
    - `server` -> 你的服务器 `ip` 地址
- 之后需要在本地项目中安装一个可以一键部署的包 `hexo-deployer-git`，命令行中执行
    ```shell
    yarn add -D hexo-deployer-git
    ```
- 之后新建一个新的 `.md` 文章
    ```shell
    hexo new 测试文章
    ```
- 开始一行命令部署了
    ```shell
    hexo g -d
    ```
  
## 遇到的问题
### 1.  服务器访问显示 `403`
- `403` 很明显是权限的问题
    >我们设置的 `/home/git/home/hexo.git` 的用户权限是 `git`，正常访问时使用的是 `root` 权限，怎么会 `403` 呢
    
    >我这边查看了一下 `/etc/nginx/nginx.conf` 文件，发现最上面默认的 `user` 设置的是 `nginx`，原来是 `nginx` 默认设置的问题，于是把这个改成 `root` 就可以了