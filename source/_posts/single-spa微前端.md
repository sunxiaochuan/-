---
title: single-spa微前端
date: 2019-09-25 17:05:46
tags: [single-spa,微前端]
categories: [软件/包的基础操作]
---

<img src="https://camo.githubusercontent.com/5082953bc69645086be2b2ac5e1a8fa20eff0314/68747470733a2f2f73696e676c652d7370612e6a732e6f72672f696d672f6c6f676f2d77686974652d6267626c75652e737667" width="200" height="200" data-canonical-src="https://single-spa.js.org/img/logo-white-bgblue.svg" style="max-width:100%;">

# 参考资料
>[single-spa github地址](https://github.com/CanopyTax/single-spa)
[single-spa 官网地址](https://single-spa.js.org/)
[single-spa 官方 demo 地址](https://single-spa.surge.sh/)

# 正文
## single-spa 是什么？
### 官方介绍百度直译

<!-- more -->

>说明
>single spa是一个javascript库，允许许多小应用程序在一个页面应用程序中共存。这个网站是一个演示应用程序，展示了什么单一应用可以做。有关single spa的更多信息，请转到 [single-spa Github page](https://github.com/CanopyTax/single-spa) 页面。
此外，这个网站的代码可以在 [single-spa-examples Github](https://github.com/CanopyTax/single-spa-examples) 中找到。下面请查看 [这个网站](https://single-spa.surge.sh/) 以下功能：
>>在react和angular应用程序之间转换而不重新加载页面。
>>>1。点击导航栏中的“反应”链接
>>>2。检查内容上的元素，查找
>>>3。点击导航栏中的“angularjs”链接
>>>4。检查内容上的元素，查找
>>延迟加载整个应用程序以获得快速的初始加载时间。
>>>1。打开开发工具的“网络”选项卡
>>>2。重新加载此页
>>>3。点击导航栏中的angularjs链接
>>>4。为angularjs应用程序的代码寻找新的网络请求
>>页面的某些部分用一个框架编写，而其他部分则使用不同的框架。
>>>1。单击导航栏中的框架检查器，以突出显示应用程序的哪些部分是在哪个框架中编写的
>>>2。检查导航栏上的元素。注意到
>>>3。转到angularjs应用程序并检查元素。
>>>这显示了一个简单的例子，一部分页面是在一个框架（react）中编写的，而另一部分是在另一个框架（angular）中编写的。当你浏览本演示中的所有其他应用程序时，你将能够看到许多不同的框架都与navbar和平共存。
>>>spa的理念是让独立的、独立的应用程序组成一个完整的页面。单spa并没有长期依赖于单个框架和每个特性，而是帮助您在开发新框架时采用它们。
{% asset_img views.png "views" %}
{% asset_img router.png "router" %}

### 说人话
简单来说就是一个万能的粘合剂，使用这个库可以让你的应用可以使用多个不同的技术栈（vue、react、angular等等）进行同步开发，最后使用一个公用的路由即可实现完美切换。
当然了，也可以使用一样的技术栈，分不同的团队进行开发，只需要最后使用这个库将其整合在一起，设置不用的路由名称即可。

## 源码部分
### 官网 demo 源码
>[源码 github 地址](https://github.com/CanopyTax/single-spa-examples)

- 最好是本地 down 一下源码，本地起个服务查看一下效果
  ```shell
  git clone git@github.com:CanopyTax/single-spa-examples.git
  cd single-spa-examples

  # Install yarn at https://yarnpkg.com/lang/en/docs/install/
  # 装包
  yarn
  # 启动服务
  yarn start
  # 手动打开地址
  open http://localhost:8080
  ```

  {% asset_img 效果图.gif "效果图" %}

- 主要的粘合各个应用的源码部分
    - `single-spa-examples.js` 文件
      ```javascript
      import {declareChildApplication, start} from 'single-spa';
      import {loadEmberApp} from 'single-spa-ember';
      import 'babel-polyfill';

      declareChildApplication('navbar', () => import('./navbar/navbar.app.js'), () => true);
      declareChildApplication('home', () => import('./home/home.app.js'), () => location.pathname === "" || location.pathname === "/");
      declareChildApplication('angularjs', () => import('./angularjs/angularjs.app.js'), pathPrefix('/angularjs'));
      declareChildApplication('react', () => import('./react/react.app.js'), pathPrefix('/react'));
      declareChildApplication('angular', () => import('./angular/angular.app.js'), pathPrefix('/angular'));
      declareChildApplication('vue', () => import('src/vue/vue.app.js'), pathPrefix('/vue'));
      declareChildApplication('svelte', () => import('src/svelte/svelte.app.js'), pathPrefix('/svelte'));
      declareChildApplication('preact', () => import('src/preact/preact.app.js'), pathPrefix('/preact'));
      declareChildApplication('iframe-vanilla-js', () => import('src/vanillajs/vanilla.app.js'), pathPrefix('/vanilla'));
      declareChildApplication('inferno', () => import('src/inferno/inferno.app.js'), pathPrefix('/inferno'));
      declareChildApplication('cyclejs', () => import('src/cyclejs/cycle.app.js'), pathPrefix('/cycle'));
      declareChildApplication('ember', () => loadEmberApp("ember-app", '/build/ember-app/assets/ember-app.js', '/build/ember-app/assets/vendor.js'), pathPrefix('/ember'));

      start();

      function pathPrefix(prefix) {
          return function(location) {
              return location.pathname.indexOf(`${prefix}`) === 0;
          }
      }
      ```
- 每个子应用都会引用 `single-spa` 写的一个相对的转换插件（应用 -> 文件名 -> 插件名），下面列举三个应用，其他的都是统一的逻辑
    - react -> /src/react/react.app.js -> single-spa-react 
    - vue -> /src/vue/vue.app.js -> single-spa-vue 
    - angular -> /src/angular/angular.app.js -> single-spa-angular 