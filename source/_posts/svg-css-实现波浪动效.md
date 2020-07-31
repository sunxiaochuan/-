---
title: svg + css 实现波浪动效
date: 2020-07-31 11:31:39
tags: [svg,css,动画]
categories: [CSS 武艺]
---
## 前言
>[参考网址](https://alvarotrigo.com/fullPage/wordpress-plugin-elementor/)
这样的需求效果在实际的应用中还是蛮常见的。

<!-- more -->

-  效果 gif 图
    >{% asset_img svg + css 实现波浪.gif "svg + css 实现波浪" %}
    ![svg + css 实现波浪.gif](https://upload-images.jianshu.io/upload_images/9064013-9ab224fb37f5bbd3.gif?imageMogr2/auto-orient/strip)


## 源码
-  `html` [github 地址](https://github.com/sunxiaochuan/simple-demo/blob/master/CSS/svg%20%2B%20css%20%E5%AE%9E%E7%8E%B0%E6%B3%A2%E6%B5%AA%E5%8A%A8%E6%95%88/svg%20%2B%20css%20%E5%AE%9E%E7%8E%B0%E6%B3%A2%E6%B5%AA%E5%8A%A8%E6%95%88.html)
    ```html
    <!DOCTYPE html>
    <html lang="en">

    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>svg + css 实现波浪</title>
      <style>
        * {
          margin: 0;
          padding: 0;
        }

        body {
          background: linear-gradient(135deg, #df5f99 0%, #492bab 100%);
          padding: 50px 0 0;
        }

        .waves {
          background: #00f;
          width: 100%;
          background: 0 0;
          position: relative;
          height: 32px;
          margin-top: 0;
          margin-bottom: -4px
        }

        .wave {
          position: absolute;
          fill: #fff;
          stroke: #fff;
          stroke-opacity: .5;
          stroke-width: 2px;
          animation: slide 10s linear infinite;
          animation-delay: 0s;
          bottom: 0
        }

        .white-bg{
          height: 500px;
          background-color: #fff;
        }

        @keyframes slide {
          0% {
            transform: translateX(0)
          }

          to {
            transform: translateX(-2000px)
          }
        }
      </style>
    </head>

    <body>
      <svg class="waves">
        <path class="wave" d="M0,16 q500,32 1000,0 t1000,0 t1000,0 t1000,0 V32 H-16 z"></path>
      </svg>
      <div class="white-bg"></div>
    </body>

    </html>
    ```