---
title: vuedraggable 实战各种小技巧(长期更新)
date: 2020-10-26 13:12:08
tags: [vuedraggable,Vue,实战各种小技巧,长期更新]
categories: [软件/包的基础操作]
---

## 前言

>`vuedraggable` 是一个基于 `Sortable.js` 库的 `Vue.js` 拖拽功能组件。

## 资料

>[npm 地址](https://www.npmjs.com/package/vuedraggable) 下载量还是蛮高的

>[github 地址](https://github.com/SortableJS/Vue.Draggable) `star` 数还是蛮多的

<!-- more -->

>[官网在线示例](https://sortablejs.github.io/Vue.Draggable/)

>[Sortable.js 库 github 地址](https://github.com/SortableJS/sortablejs)

### 简单的安装与使用

1.  安装

    ```shell
    yarn add vuedraggable
    # or
    npm i -S vuedraggable
    ```

2.  使用（源码出处 [custom-clone](https://github.com/SortableJS/Vue.Draggable/blob/master/example/components/custom-clone.vue)）

    ```vue
    <template>
      <div class="row">
        <div class="col-3">
          <h3>Draggable 1</h3>
          <draggable
            class="dragArea list-group"
            :list="list1"
            :group="{ name: 'people', pull: 'clone', put: false }"
            :clone="cloneDog"
            @change="log"
          >
            <div class="list-group-item" v-for="element in list1" :key="element.id">
              {{ element.name }}
            </div>
          </draggable>
        </div>

        <div class="col-3">
          <h3>Draggable 2</h3>
          <draggable
            class="dragArea list-group"
            :list="list2"
            group="people"
            @change="log"
          >
            <div class="list-group-item" v-for="element in list2" :key="element.id">
              {{ element.name }}
            </div>
          </draggable>
        </div>

        <rawDisplayer class="col-3" :value="list1" title="List 1" />

        <rawDisplayer class="col-3" :value="list2" title="List 2" />
      </div>
    </template>

    <script>
    import draggable from "@/vuedraggable";
    let idGlobal = 8;
    export default {
      name: "custom-clone",
      display: "Custom Clone",
      order: 3,
      components: {
        draggable
      },
      data() {
        return {
          list1: [
            { name: "dog 1", id: 1 },
            { name: "dog 2", id: 2 },
            { name: "dog 3", id: 3 },
            { name: "dog 4", id: 4 }
          ],
          list2: [
            { name: "cat 5", id: 5 },
            { name: "cat 6", id: 6 },
            { name: "cat 7", id: 7 }
          ]
        };
      },
      methods: {
        log: function(evt) {
          window.console.log(evt);
        },
        cloneDog({ id }) {
          return {
            id: idGlobal++,
            name: `cat ${id}`
          };
        }
      }
    };
    </script>
    <style scoped></style>

    ```


### 项目使用中具体需要注意的细节

1.  当使用两个拖拽组件，需要向目标组件拖拽时无效。

    >当使用两个拖拽组件，需要向目标组件拖拽时，需要注意：两个字段值，它们的值必须得是相同的。
    
    >这样的话，两个组件的拖拽功能才能生效，具体如下：

    -  拖拽组件
    {% asset_img 拖拽组件.png "拖拽组件" %}

    -  目标组件
    {% asset_img 目标组件.png "目标组件" %}




