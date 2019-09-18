---
title: bootstrap-fileinput 在 vue-cli 项目中的使用
date: 2018-05-11 11:20:26
updated: 2018-05-25 11:44:18
tags: [bootstrap-fileinput,插件,vue-cli,vue,bootstrap]
categories: [代码/技能进阶]
---

# 资料
>[参考地址](https://blog.csdn.net/u012157999/article/details/53150845)
[插件 github 地址](https://github.com/kartik-v/bootstrap-fileinput)

# 装包
  ```shell
  npm install bootstrap-fileinput bootstrap --save
  ```
# 演示 gif 因为接口的原因失败了，但是并不影响示例的过程 
> {% asset_img 演示效果图1.gif "演示效果图1" %}

<!-- more -->


# 示例源码
-  `vue -> template` 部分代码
  ```javascript
  <div class="form-group row">
          <label for="userIDImageFront" class="col-sm-3">身份证正面：</label>
          <div class="col-sm-5">
              <input id="userIDImageFront" type="file" class="file" data-preview-file-type="text" required name="imgPath">
          </div>
          <img class="col-sm-4" src="@/assets/img/frontPic.png" alt="样图" />
        </div>
        <div class="form-group row">
          <label for="userIDImageBack" class="col-sm-3">身份证反面：</label>
          <div class="col-sm-5">
            <input id="userIDImageBack" type="file" class="file" data-preview-file-type="text" required name="imgPath">
          </div>
          <img class="col-sm-4" src="@/assets/img/reversePic.png" alt="样图" />
        </div>
        <div class="form-group row">
          <label for="userIDSIM" class="col-sm-3">身份证SIM卡手持：</label>
          <div class="col-sm-5">
              <input id="userIDSIM" type="file" class="file" data-preview-file-type="text" required name="imgPath">
          </div>
          <img class="col-sm-4" src="@/assets/img/handPic.png" alt="样图" />
        </div>
  ```
-  `.vue ->  script`  部分代码，上面 data 便不展示了，这里重点演示的是自动上传的代码 里面有详细的参数配置定义
  ```javascript
  import $ from 'jquery'
  require('bootstrap-fileinput/js/fileinput.js') // 引入图片上传插件  input 的逻辑全部都写在了这个文件内部了  需要注意！！！
  require('bootstrap-fileinput/js/locales/zh.js') // 引入图片插件的汉化包
  require('bootstrap-fileinput/themes/fa/theme.js') // 引入主题包
  require('bootstrap/dist/js/bootstrap.js') // 引入 bootstrap

  // export default{} 的代码片段
  data(){
    return{
      // 图片上传接口
      imgUploadAPI: 'xxx'
    }
  }

  mounted:{
    // 初始化图片上传控件
      me.initInputFile($('input.file[type=file]'), me.imgUploadAPI)
  }

  methods:{
    // 初始化图片上传控件
      initInputFile: function(eles, posturl) {
        const me = this
        let $input = eles
        if ($input.length) {
          $input
            .fileinput({
              /**
               * theme icon 主题 需要引入相应的主题包
               * language 语言设置 需要引入相应的语言包
               * uploadUrl 上传路径
               * showCaption 是否展示 input 文字的说明 -- 标题
               * showUpload 是否显示上传按钮
               * showRemove 是否可以删除
               * dropZoneEnabled 是否开启拖拽上传功能
               * maxFileCount 最多的文件数量
               * maxFileSize 最大的尺寸
               * allowedFileExtensions 允许的文件扩展名
               */
              theme: 'fa',
              language: 'zh',
              uploadUrl: posturl,
              showUpload: false,
              showRemove: false,
              dropZoneEnabled: false,
              maxFileCount: 1,
              allowedFileExtensions: ['jpg', 'png', 'gif']
            })
            // 实现图片被选中后自动提交
            .on('filebatchselected', function(event, files) {
              // 选中事件
              $(event.target).fileinput('upload')
            })
            .on('fileuploaded', function(event, data) {
              // 提交成功之后
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
            })
        }
      },
  }
  ```
## 更新
-  问题
  > 由于在上传时未在 html 中写 `file` 文件的 `name` 属性值，从而导致数据无法传递
-  解决方法
  ```html
  <input id="userIDImageBack" type="file" class="file" data-preview-file-type="text" required name="imgPath">
  ```
  > 需要注意的是这个 `name` 属性的值不是随便写的，而是需要与后台写的保持一致，这个需要询问后台定义的参数名称

-  gif 图演示
  > {% asset_img 演示效果图2.gif "演示效果图2" %}