---
title: bootstrap-fileinput 进阶 -- 实现上传失败清除之前的预览图且可以继续上传
date: 2018-05-17 17:25:48
tags: [bootstrap-fileinput,插件,bootstrap,bug]
categories: [代码/技能进阶]
---
# 最终实现的 GIF 效果图
> {% asset_img 演示效果图.gif "演示效果图" %}

# 资料
> [某个老哥写的 API 博客](https://blog.csdn.net/u012526194/article/details/69937741)
[官方方法 API 地址](http://plugins.krajee.com/file-input/plugin-methods)

# 正文
> 需求：在文件上传之后（接口可以正常的访问，只是返回结果是失败的情况下），这个时候需要将原来生成的缩略图清除掉（因为展示的样式会让用户看起来是成功的样子），还要使这个上传空间可以正常的使用（这个我查了好久的资料，用看了源码里的方法，几个方法都试了下最终才成功的）

## 源码
> [先得看下之前的一篇入门笔记 -- 引入插件并实现自动上传功能](https://www.jianshu.com/p/996699977f1c)
-  js 较上篇笔记扩展的部分
  ```javascript
  if ($input.length) {
          $input
            .fileinput({
              /**
               * theme icon 主题 需要引入相应的主题包
               * language 语言设置 需要引入相应的语言包
               * uploadUrl 上传路径  可不写在下面与表单一起手动上传
               * showCaption 是否展示 input 文字的说明 -- 标题
               * showUpload 是否显示上传按钮
               * showRemove 是否可以删除
               * dropZoneEnabled 是否开启拖拽上传功能
               * maxFileCount 最多的文件数量
               * maxFileSize 最大的尺寸
               * allowedFileExtensions 允许的文件扩展后缀名
               * autoReplace 是否自动替换当前图片，设置为true时，再次选择文件， 会将当前的文件替换掉
               */
              theme: 'fa',
              language: 'zh',
              uploadUrl: posturl,
              showUpload: false,
              showRemove: true,
              dropZoneEnabled: false,
              maxFileCount: 1,
              allowedFileExtensions: ['jpg', 'png'],
              autoReplace: true
            })
            // 实现图片被选中后自动提交
            .on('filebatchselected', function(event, files) {
              // 选中事件
              $(event.target).fileinput('upload')
            })
            // 异步上传错误结果处理
            .on('fileerror', function(event, data, msg) {
              // 清除当前的预览图 ，并隐藏 【移除】 按钮
              $(event.target)
                .fileinput('clear')
                .fileinput('unlock')
              $(event.target)
                .parent()
                .siblings('.fileinput-remove')
                .hide()
              // 打开失败的信息弹窗
              me.openAlertModel('请求失败，请稍后重试')
            })
            // 异步上传成功结果处理
            .on('fileuploaded', function(event, data) {
              // 判断 code 是否为  0    0 代表成功
              const getData = data.response
              console.log(getData)
              if (getData.code === 0) {
                let eleID = $(event.target).prop('id')
                // console.log(eleID)
                // 通过 ID 判断给相应的字段赋值
                if (eleID === 'userIDImageFront') {
                  // 正面
                  me.postData.frontPic = JSON.parse(getData.result).url
                } else if (eleID === 'userIDImageBack') {
                  // 背面
                  me.postData.reversePic = me.postData.frontPic = JSON.parse(
                    getData.result
                  ).url
                } else if (eleID === 'userIDSIM') {
                  // 手持
                  me.postData.handPic = me.postData.frontPic = JSON.parse(
                    getData.result
                  ).url
                }
              } else {
                // 失败回调
                // 清除当前的预览图 ，并隐藏 【移除】 按钮
                $(event.target)
                  .fileinput('clear')
                  .fileinput('unlock')
                $(event.target)
                  .parent()
                  .siblings('.fileinput-remove')
                  .hide()
                // 打开失败的信息弹窗
                me.openAlertModel('请求失败，请稍后重试')
              }
            })
        }
  ```
-  总结：
  > 主要使用的 `clear` 和 `unlock` 两个插件中定义的方法