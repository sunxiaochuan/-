---
title: chocolatey 安装和使用
date: 2018-05-14 11:05:36
tags: [chocolatey,安装工具,教程,windows]
categories: [软件/包的基础操作]
---

# 资料

> [chocolatey 官网](https://chocolatey.org/)

> [chocolatey 安装指南 ](https://chocolatey.org/install)

# 安装

* 打开命令行工具输入以下命令，即可自行安装，需稍作等待安装时间，期间可能会被 360 杀毒软件拦截，允许全部 即可

```
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

# 使用

* 这里以安装 yarn 为例

```
# 查看是否安装成功
choco -v
choco  install yarn
```

* 常用命令行

```
#  安装
choco install
# 升级
choco  upgrade
```
