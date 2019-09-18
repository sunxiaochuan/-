---
title: 多级菜单小demo
date: 2018-05-16 10:59:45
tags: [demo,多级菜单]
categories: [代码/技能进阶]
---

# 说明

> 这里只贴下 html 和 js 了，css 较为简单，里面的一些类名是基于 [bootstrap](http://www.bootcss.com/) 框架的

# 源码

- html

  ```html
  <ul class="nav nav-pills flex-column framework-list">
      <li>
        <i class="glyphicon glyphicon-triangle-bottom"></i>
        <span role="button">组织架构</span>
        <ul>
          <li>
            <i class="glyphicon glyphicon-triangle-bottom"></i>
            <span role="button">XXZ集团公司</span>
            <ul>
              <li>管理层</li>
              <li>研发部</li>
              <li>市场部</li>
              <li>行政部</li>
            </ul>
          </li>
        </ul>
      </li>
    </ul>
  ```

- js 这个是基于的 [jQuery](https://www.jquery123.com/) 的写法

  ```javascript
  $('.framework-list li:has(ul)').click(function(e) {
      e.stopPropagation()
      const ul = $(this).find('> ul')
      if (ul.is(':visible')) {
        ul.hide('fast')
      } else if (ul.is(':hidden')) {
        ul.show('fast')
      }
    })
  ```

- 效果图：
  > {% asset_img 效果图.gif "效果图" %}