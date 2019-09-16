---
title: vue DOM 事件修饰符
date: 2018-05-10 15:43:54
tags: [vue-cli,vue,技巧,框架,三大框架之一]
categories: [代码/技能进阶]
---

## DOM 事件修饰符

    ```
    <!-- 阻止单击事件继续传播 -->
    <a v-on:click.stop="doThis"></a>

    <!-- 提交事件不再重载页面 -->
    <form v-on:submit.prevent="onSubmit"></form>

    <!-- 修饰符可以串联 -->
    <a v-on:click.stop.prevent="doThat"></a>

    <!-- 只有修饰符 -->
    <form v-on:submit.prevent></form>

    <!-- 添加事件监听器时使用事件捕获模式 -->
    <!-- 即元素自身触发的事件先在此处处理，然后才交由内部元素进行处理 -->
    <div v-on:click.capture="doThis">...</div>

    <!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
    <!-- 即事件不是从内部元素触发的 -->
    <div v-on:click.self="doThat">...</div>
    ```

* 示例，如下图所示，这样写的话点击了 li 内部的元素的话不会影响 li 的 click 的点击事件
  > ![image.png](https://upload-images.jianshu.io/upload_images/9064013-9a06bab7ca000e27.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
