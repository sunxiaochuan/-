---
title: uni-app 踩坑之路(长期更新)
date: 2020-07-21 17:37:05
tags: [uni-app,踩坑之路]
categories: [软件/包的基础操作]
---
## 资料
>[`uni-app` 官网](https://uniapp.dcloud.net.cn/)

## 正文

<!-- more -->

### 1.  基本创建并启动工程操作
>[原文地址](https://uniapp.dcloud.net.cn/quickstart?id=_2-%e9%80%9a%e8%bf%87vue-cli%e5%91%bd%e4%bb%a4%e8%a1%8c)
-  项目的创建
    ```shell
    # 全局安装脚手架的两种方式
    npm install -g @vue/cli
    # OR
    yarn global add @vue/cli

    # 新建工程 => 选择`默认模板`即可
    vue create -p dcloudio/uni-preset-vue my-project
    ```
-  项目的启动（本地启动微信小程序服务）
    ```shell
    # 本地启动微信小程序服务
    yarn dev:mp-weixin
    ```
-  之后手动在微信开发者工具中导入该项目，一次选中 `my-project => dist => dev => mp-weixin` 目录点击确定即可

### 2.  安装 `sass-loader` 之后，由于版本过高，导致报错无法成功编译
-  为了使用 `sass` 安装相应需要的依赖
    ```shell
    yarn add node-sass sass-loader -D
    ```
-  由于我安装的 `sass-loader` 是 `9.0.2` 版本的，导致无法正常编译，报错信息 `options has an unknown property 'prependData'. These properties are valid:`，解决方法修改版本号 `9.0.2 => 8.0.2`，重新安装依赖
    >[该问题参考文章："【已解决】uniapp项目,通过cli指令新建的项目,在任意页面style标签使用lang="scss"报错:options has an unknown property 'prependData'"](https://ask.dcloud.net.cn/question/101104)

### 3.  微信小程序底部的 `icon` 

1.   `icon` 尺寸需要是 `81*81` 的，不然会非常模糊尺寸需要是 `81*81` 的，不然会非常模糊
        >[参考文章：小程序底部的tabbar图片显示老是会模糊，不管放多大的图都模糊，什么原因](https://segmentfault.com/q/1010000009630810/a-1020000009630903)
        -  对比图
        {% asset_img 对比图.png "对比图" %}

2.   `icon` 的周围要适当的留白，不能全部填满，不然不好看
        -  示意图，如下所示对比非常的明显
        {% asset_img 示意图.png "示意图" %}

### 4.  微信小程序相关的语法，在应用中中需要注意的地方

1.  `image` 标签高度随宽度自适应
    ```html
    <image mode="widthFix" />
    ```

2.  `image` 标签宽高自适应铺满，但是会裁切掉部分的图片
    ```html
    <image mode="aspectFill" />
    ```

3.  `scroll-view` 页面下拉滚动组件
    ```vue
    <template lang="pug">
        scroll-view.home(@scrolltolower="handelToLower" scroll-y)
    </template>

    <script>
        export default {
            methods: {
                /**
                * 页面内容滚动到底部 回调函数
                */
                handelToLower() {
                   console.log("到底部啦！");
                }
            },
        }
    </script>
    ```
    -  `scss` 需要特殊设置
        ```scss
        .home {
        // 小程序使用
        height: 100vh;
        // #ifdef  H5
        // 减去顶部标题和底部导航的高度，与微信小程序保持一致，会覆盖上方的设置
        height: calc(100vh - 44px - 50px);
        }
        ```
    -  当内部内容有 `flex` 布局的话，需要在属性中增加 `enable-flex`，否则无效
    

4.  `swiper` 轮播图组件
    ```vue
    <template lang="pug">
        swiper(autoplay indicator-dots circular)
            swiper-item(v-for='item in bannerList' :key="item.url")
            image(:src="item.url")
    </template>

    <script>
        export default {
            data() {
                return {
                    bannerList: [
                        {
                        url:
                            "https://img.alicdn.com/tfs/TB1g4DmcggP7K4jSZFqXXamhVXa-520-280.jpg_q90_.webp"
                        },
                        {
                        url:
                            "https://img.alicdn.com/simba/img/TB13oCCSpXXXXctaXXXSutbFXXX.jpg"
                        },
                        {
                        url:
                            "https://img.alicdn.com/simba/img/TB1b2svaODsXe8jSZR0SutK6FXa.jpg"
                        },
                        {
                        url:
                            "https://img.alicdn.com/simba/img/TB1x3imuXY7gK0jSZKzSuuikpXa.jpg"
                        },
                        {
                        url:
                            "https://img.alicdn.com/tfs/TB18NsRcsVl614jSZKPXXaGjpXa-520-280.jpg_q90_.webp"
                        }
                    ]
                };
            }
        };
    </script>
    ```
    -  `scss` 需要特殊处理一下
        ```scss
        .swiper-content {
        swiper {
            // 1.9 是 banner 图片的宽高比例 520/280 = 1.8571428571428572
            height: calc(750rpx / 1.9);
            image {
            height: 100%;
            }
        }
        }
        ```

5.  `uni-segmented-control` 分段器组件
    ```vue
    <template lang="pug">
        .home-tab
            .tab-title-list
            uni-segmented-control(:current="current" :values="items.map(v => v.title)" @clickItem="onClickItem" style-type="text" active-color="#2b7bff")
            .tab-title-search
        .home-content
            home-recommend(v-if="current === 0")
            home-category(v-if="current === 1")
            home-new(v-if="current === 2")
            home-album(v-if="current === 3")
    </template>

    <script>
        import homeAlbum from "@/pages/home/home-album";
        import homeCategory from "@/pages/home/home-category";
        import homeNew from "@/pages/home/home-new";
        import homeRecommend from "@/pages/home/home-recommend";
        import { uniSegmentedControl } from "@dcloudio/uni-ui";
        export default {
            components: {
                homeAlbum,
                homeCategory,
                homeNew,
                homeRecommend,
                uniSegmentedControl
            },
            data() {
                return {
                    items: [
                        {
                        title: "推荐"
                        },
                        {
                        title: "分类"
                        },
                        {
                        title: "最新"
                        },
                        {
                        title: "专辑"
                        }
                    ],
                    current: 0
                };
            },
            methods: {
                /**
                * tab 切换 回调函数
                */
                onClickItem(e) {
                    if (this.current !== e.currentIndex) {
                        this.current = e.currentIndex;
                    }
                }
            }
        };
    </script>
    ```

6.  `navigator` 链接跳转功能
    ```vue
    <template lang="pug">
        navigator(url="/pages/home/home-album/details")
            text 测试
    </template>
    ```
    >这个跳转的地址与 `pages.json` 中设置的 `pages => path` 属性值保持一致。需要注意的是：不可以和 `tabBar` 中使用的 `pagePath` 一致，否则无效。

7.  `text` 标签可以识别数据中的转义字符，如 `\n` 会识别为换行符

8.  `video` 标签
    -   视频预览图充满整个容器的属性，默认是正常的比例展示的
        ```vue
        video(objectFit="fill")
        ```
    -   `muted` 这个 `Boolean` 属性控制视频的声音开关
        ```vue
        video(:muted="false")
        ```

9.  `button` 标签
    -   设置分享，使用微信小程序的内置功能
        ```vue
        button(open-type="share") 分享
        ```

### 5.  为 `H5` 方式的服务，设置代理，防止浏览器拦截接口请求

1.  `manifest.json` 文件，增加 h5特有相关 配置
    ```json
	/* h5特有相关 */
	"h5": {
		"devServer": {
			"port": 8000, //端口号
			"disableHostCheck": true,
			"proxy": {
				"/api": {
					"target": "http://xxxx.cn", //目标接口域名
					"ws": true, // proxy websockets
					"changeOrigin": true, //是否跨域
					"pathRewrite": {
						"^/api": ""
					}
				}
			}
		}
	}
    ```
-  使用演示
    ```javascript
    wx.request({
    url: "api/xxxxx",
    success(res) {
        console.log(res)
    }
    })
    ```

2.  需要注意的是，这样写微信小程序是不会识别的，所以还需要使用官方文档中的 [条件编译](https://uniapp.dcloud.io/platform?id=%e6%9d%a1%e4%bb%b6%e7%bc%96%e8%af%91) 的方式来进行处理，下文中可查看具体的使用方式


### 6.  使用 `条件编译` 的方式，对某个平台单独设置

1.  完善上方接口请求方式
-  `main.js` 文件，增加全局变量（也可以在 `APP.vue` 文件中使用 `globalData` 的方式增加全局变量）
    ```javascript
    // 条件编译，设置相应环境的变量值 https://uniapp.dcloud.io/platform?id=%e6%9d%a1%e4%bb%b6%e7%bc%96%e8%af%91
    // #ifdef  MP-WEIXIN
    // 接口请求地址
    Vue.prototype.APINAME = "http://xxx.cn"
    // #endif

    // #ifdef  APP-PLUS || H5
    // 使用 manifest.json 中的 devServer 代理配置，防止浏览器阻拦接口请求
    Vue.prototype.APINAME = "api"
    // #endif
    ```
-  使用演示
    ```javascript
    wx.request({
    url: `${this.APINAME}/xxxxx`,
    success(res) {
        console.log(res)
    }
    })
    ```

2.  在样式代码中使用条件编译
    >由于 `100vh` 在微信小程序和 `H5` 两个环境中不一样的问题，才有了这样的需求
    
    ```scss
    .home {
    // 小程序使用
    height: 100vh;
    // #ifdef  H5
    // 减去顶部标题的高度，会覆盖上方的设置
    height: calc(100vh - 44px);
    }
    ```