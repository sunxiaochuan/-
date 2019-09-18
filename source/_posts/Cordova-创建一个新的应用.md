---
title: Cordova-创建一个新的应用
date: 2019-09-12 12:28:56
tags: [Cordova]
categories: []
---


# 资料
>[Cordova 官网文档](https://cordova.apache.org/docs/en/latest/guide/cli/index.html) 详细的文档可点击查看

# 正文
### 1.  环境配置

<!-- more -->

1.  前提条件（我的是 windows 系统）
-  安装 [nodejs](http://nodejs.cn/download/)
-  安装 [Android Studio](https://developer.android.com/studio/)
-  使用 [Android Studio](https://developer.android.com/studio/) 安装 Android 模拟器
-  安装 [VS Code](https://code.visualstudio.com/) 用来进行轻量开发
-  安装 [Java SDK 1.8.0](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 这是个大坑！！！其他版本的不好使
2.  环境变量的配置
>我的是 windows 系统，所以需要在 【我的电脑】-> 【右键属性】-> 【高级系统设置】 -> 【环境变量】 -> 【新建】进行添加
```
# 下面的是 需要添加的变量名 -> 相应的目录（我的安装路径）
ANDROID_HOME -> D:\AndriodSDk
JAVA_HOME -> D:\Program Files\Java\jdk
Path -> 追加(注意分号) D:\Program Files\Java\jdk\bin;
```
-  配好了上述的环境变量之后，才可以使用相关的命令行噢~，可自行在命令行使用 `java` 和 `javac` 进行测试是否配置成功
### 2.  创建应用
1.  命令行依次输入以下命令，启动项目
```shell
# 全局安装 `Cordova CLI`
npm install -g cordova

# 创建项目
cordova create hello com.example.hello HelloWorld

# 添加平台
cordova platform add android

# 运行项目在模拟器/真机进行调试
cordova run android
```
2.  常用的命令行命令记录（具体解释可查看最上方的官网文档）
```shell
# 全局安装 `Cordova CLI`
npm install -g cordova

# 创建项目
cordova create hello com.example.hello HelloWorld

# 添加平台
cordova platform add android
cordova platform add ios

# 查看构建项目的条件是否具备
cordova requirements

# 为所有平台/单个平台构建项目
cordova build
cordova build android

# 测试应用程序
cordova emulate android

# 运行项目在模拟器/真机进行调试
cordova run android

# 添加插件
cordova plugin add cordova-plugin-camera

# 在本地浏览器中运行
cordova serve

# 检查当前的平台集
cordova platform ls
```
