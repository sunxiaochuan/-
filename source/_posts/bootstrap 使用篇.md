---
title: bootstrap 使用篇
date: 2018-05-11 18:12:54
tags: [bootstrap,教程]
categories: [软件/包的基础操作]
---

# 前言
> 本篇笔记只是简单的一个使用中的小总结，真的很简单，目的是为了以后方便查阅。

## 准备工作
- 装包
  ```shell
  npm install boostrap --save
  ```

- 引用
  ```shell
  import 'bootstrap/dist/css/bootstrap.css'
  import 'bootstrap' // 引入 bootstrap
  ```

<!-- more -->


# 资料
> [官方文档](https://v4.bootcss.com/docs/4.0/getting-started/introduction/)
# 正文
## 分页的使用
> [参考文档地址](https://v4.bootcss.com/docs/4.0/components/pagination/) 详细的示例都在这里的，下面只是一个简单的示例
- 示例代码
  ```html
  <nav aria-label="...">
    <ul class="pagination">
      <li class="page-item disabled">
        <a class="page-link" href="#" tabindex="-1">Previous</a>
      </li>
      <li class="page-item"><a class="page-link" href="#">1</a></li>
      <li class="page-item active">
        <a class="page-link" href="#">2 <span class="sr-only">(current)</span></a>
      </li>
      <li class="page-item"><a class="page-link" href="#">3</a></li>
      <li class="page-item">
        <a class="page-link" href="#">Next</a>
      </li>
    </ul>
  </nav>
  ```
- 效果图 
  > {% asset_img 效果图.png "效果图" %}
## 弹窗的使用
> [参考文档地址](https://getbootstrap.com/docs/4.0/components/modal/) 里面有多种弹窗的源码示例，也有相应的参数说明
- 源码示例
  ```html
  <!-- Button trigger modal -->
  <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">
    Launch demo modal
  </button>

  <!-- Modal -->
  <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          ...
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
          <button type="button" class="btn btn-primary">Save changes</button>
        </div>
      </div>
    </div>
  </div>
  ```
- 效果图 gif
  > {% asset_img 效果图.gif "效果图" %}
- 这里我将这个弹窗作为单独的用户操作结果展示来用，`html` 结构只是用到了 `modal`
  ```html
  <!-- 弹窗 -->
      <div class="modal fade" tabindex="-1" role="dialog" id="myModal">
        <div class="modal-dialog" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <!-- <h5 class="modal-title"></h5> -->
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
              <p>{{ modalMsg }}</p>
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-primary" data-dismiss="modal">确定</button>
              <button type="button" class="btn btn-secondary" data-dismiss="modal">关闭</button>
            </div>
          </div>
        </div>
      </div>
  ```
- 主要的 `API`
  ```javascript
  // 打开弹窗
  $('#myModal').modal('show')
  // 关闭弹窗
  $('#myModal').modal('hide')
  ```
