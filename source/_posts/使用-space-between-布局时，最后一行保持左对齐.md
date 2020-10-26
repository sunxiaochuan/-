---
title: 使用 space-between 布局时，最后一行保持左对齐
date: 2020-10-26 13:28:48
tags: [css,space-between]
categories: [CSS 武艺]
---

## 资料

>[让CSS flex布局最后一行列表左对齐的N种方法 -- 张鑫旭博客](https://www.zhangxinxu.com/wordpress/2019/08/css-flex-last-align/)

<!-- more -->

## 实现方式
>引用的资料中各种情况包含的实现方式基本都是有的，这里只记录一下我自己所使用的到的方式——“如果每一行列数不固定”

>“如果每一行的列数不固定，则上面的这些方法均不适用，需要使用其他技巧来实现最后一行左对齐。
这个方法其实很简单，也很好理解，就是使用足够的空白标签进行填充占位，具体的占位数量是由最多列数的个数决定的，例如这个布局最多7列，那我们可以使用7个空白标签进行填充占位，最多10列，那我们需要使用10个空白标签。”

-  `Pug` 模板引擎的 `HTML` 代码
    ```pug
    <template lang="pug">
    .data-list
      .data-item(v-for="item in dataListData" :key="item.id")
      i
      i
      i
    </template>
    ```

-  `CSS` 代码
    ```stylus
    <style lang="stylus" scoped>
    .data-list
      padding 10px 0 5px
      display flex
      flex-wrap wrap
      justify-content space-between
      align-content baseline
      min-height 100 * 4 + 14 * 4 + 10 * 2
      margin-right -16px
      &>i
        width (264 / (853 - 16 * 2) * 100)%
        margin-right auto
      .data-item
        max-width (264 / (853 - 16 * 2) * 100)%
        min-width 100px
        flex 1 1 (264 / (853 - 16 * 2) * 100)%
        height 100px
        cursor pointer
        margin 0 auto 14px 0
    </style>
    ```


-  演示 Gif 图
     
    {% asset_img 使用-space-between-布局时，最后一行保持左对齐.gif "使用-space-between-布局时，最后一行保持左对齐" %}
