---
title: vue-echarts 的使用与踩坑
date: 2020-07-15 11:26:21
tags: [vue-echarts,教程]
categories: [软件/包的基础操作]
---

## 资料
>[`npm` 地址](https://www.npmjs.com/package/vue-echarts)
[`github` 地址](https://github.com/ecomfe/vue-echarts)

## 正文

<!-- more -->

### 1.  简单的使用
-  安装

```shell
$ npm install echarts vue-echarts

# 或者使用 yarn 装
$ yarn add echarts vue-echarts
```

-  `main.js` 中引入

```javascript
import Vue from 'vue'
import ECharts from 'vue-echarts'

// 手动导入ECharts模块以减小包的大小
import 'echarts/lib/chart/bar'
import 'echarts/lib/component/tooltip'

// 如果要使用ECharts扩展，只需导入扩展包即可使用
// 以ECharts-GL为例：
// 您只需要使用`npm install --save echarts-gl`和按如下方式
import 'echarts-gl'

// 注册组件以使用
Vue.component('v-chart', ECharts)
```

-  `index.vue` 文件中使用（以下是官网提供的 Demo 源码 [查看地址](https://github.com/ecomfe/vue-echarts/tree/master/src/demo)）

```vue
<template>
<v-chart :options="polar"/>
</template>

<style>
/**
 * The default size is 600px×400px, for responsive charts
 * you may need to set percentage values as follows (also
 * don't forget to provide a size for the container).
 */
.echarts {
  width: 100%;
  height: 100%;
}
</style>

<script>
import ECharts from 'vue-echarts'
import 'echarts/lib/chart/line'
import 'echarts/lib/component/polar'

export default {
  components: {
    'v-chart': ECharts
  },
  data () {
    let data = []

    for (let i = 0; i <= 360; i++) {
        let t = i / 180 * Math.PI
        let r = Math.sin(2 * t) * Math.cos(2 * t)
        data.push([r, i])
    }

    return {
      polar: {
        title: {
          text: '极坐标双数值轴'
        },
        legend: {
          data: ['line']
        },
        polar: {
          center: ['50%', '54%']
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross'
          }
        },
        angleAxis: {
          type: 'value',
          startAngle: 0
        },
        radiusAxis: {
          min: 0
        },
        series: [
          {
            coordinateSystem: 'polar',
            name: 'line',
            type: 'line',
            showSymbol: false,
            data: data
          }
        ],
        animationDuration: 2000
      }
    }
  }
}
</script>
```

### 2.  问题的记录

1.  `Cannot assign to read only property 'exports' of object '#<Object>'` 昨天在装完包之后，试过还没事情，今天一来就跑不起来了
> {% asset_img bug.png "bug 截图" %}

>查看到是 `vue-echarts` 中 引用的 `lodash-es` 报的错误，网上检索之后，大致意思是：和 `webpack` 的版本有关系，混用 `import` 和 `module.exports` 导致的错误，[该问题的讨论地址](https://github.com/webpack/webpack/issues/4039)

-  解决方法

>最简单的方法是把设置使用 `babel` 转换 `vue-echarts` 代码的地方注释掉，`vue.config.js` 文件中操作
> {% asset_img caozuo1.png "操作截图" %}
但是这样也是会导致，代码的兼容性很差，只兼容最新版本的浏览器

>最优的方法是在 `babel.config.js` 添加一行配置，[解决方案提供的地址](https://github.com/ecomfe/vue-echarts/issues/213#issuecomment-528741715)
```javascript
module.exports = {
  presets: ['@vue/app'],
  sourceType: 'unambiguous', // 添加这行
}
```
-  以下是 [`babel `官网提供的 `sourcetype` 参数文档](https://babeljs.io/docs/en/options#sourcetype)
>  ### `sourceType`

    类型：`"script" | "module" | "unambiguous"`
    默认：“module”

    *   `"script"`-使用ECMAScript脚本语法解析文件。不允许`import`/ `export`语句，并且文件不在严格模式下。
    *   `"module"`-使用ECMAScript模块语法分析文件。文件是自动严格的，并且允许`import`/ `export`语句。
    *   `"unambiguous"`-如果存在`import`/ `export`语句，则将文件视为“模块” ，否则将其视为“脚本”。

    `unambiguous`在类型未知的上下文中可以非常有用，但是会导致错误匹配，因为拥有不使用`import`/ `export` 语句的模块文件是完全有效的。

    此选项很重要，因为当前文件的类型会影响输入文件的解析以及可能希望向当前文件添加`import`/ `require`使用的某些转换 。

    例如，[`@babel/plugin-transform-runtime`](https://babeljs.io/docs/en/babel-plugin-transform-runtime) 依靠当前文档的类型来决定是插入`import`声明还是`require()`调用。 [`@babel/preset-env`](https://babeljs.io/docs/en/babel-preset-env)其[`"useBuiltIns"`](https://babeljs.io/docs/en/babel-preset-env#usebuiltins)选择也相同 。由于Babel默认将文件视为ES模块，因此通常这些插件/预设将插入`import`语句。设置正确的`sourceType`值很重要，因为错误的类型可能导致Babel将`import`语句插入到本应为CommonJS文件的文件中的情况。这在`node_modules`正在执行依赖项编译的项目中尤其重要，因为插入 `import`语句可能导致Webpack和其他工具将文件视为ES模块，从而破坏了原本可以正常工作的CommonJS文件。

    注意：此选项不会影响`.mjs`文件的解析，因为它们目前已被硬编码为始终解析为`"module"`文件。


