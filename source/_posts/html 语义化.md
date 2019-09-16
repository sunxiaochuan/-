---
title: html 语义化
date: 2018-05-21 19:50:59
tags: [html,语义化,基础,知识]
categories: [代码/技能进阶,一灯学堂]
---

# 资料

> [理解 HTML 语义化](https://www.cnblogs.com/fliu/articles/5244866.html)

# 语义化的目的

> 语义化是为了更好的 [seo 搜索引擎优化](https://baike.baidu.com/item/%E6%90%9C%E7%B4%A2%E5%BC%95%E6%93%8E%E4%BC%98%E5%8C%96/3132?fromtitle=seo&fromid=102990&fr=aladdin)

# 需要注意的地方

1.  使用 `div` 来进行布局，不要用 `div` 进行无意义的包裹（比如：段落文字之类的要使用 `p` 标签），尽量也不要用无意义的标签 span
2.  在语义化不明显时，既可以使用 `div` 或者 `p` 时，尽量用 `p`，因为 `p` 在默认情况下有上下间距，对兼容特殊终端有利。
3.  需要强调的文本尽量使用 `css`来战士，`strong` 是粗体，`em` 是斜体
4.  **（现在已经不是非常必要的东西）**使用表格的时候，标题要用 `caption` 表头用`thead`，主体部分用 `tbody` 包裹，尾部用 `tfoot` 包裹，表头和一般单元格要区分开，表头用 `th`，单元格用 `td`
5.  `input` 的话最好是和 `label` 配合着使用，这个是有助于用户体验的
6.  对某个标题的解释 `dl -> dd(标题) -> dt(解释内容)`
7.  有序列表 `ol -> li` ，无序列表 `ul -> li`
8.  尽量少写 `html` 标签，一定要少写，好处：减少 `DOM` 渲染的时间，节省文件的大小

    > 可以使用伪元素 `::after` 和 `::before` 来尽量减少 `html` 标签的数量<br>一个 `html` 标签最次最次得顶三个元素

# `html5`

1.  新增的语义化标签

    ```
    header 头部 ->  nav 导航
    article 文章  ->  section  ->  h1 / p
    footer  底部
    aside 侧边
    ```

    > 现在最终演化出来的比较常用的页面结构

    ```
    <header>
        <nav></nav>
    </header>
    <div>
        <section>1楼</section>
        <section>2楼</section>
        <section>3楼</section>
        <aside>侧边栏</aside>
        <address>地址</address>
    </div>
    <footer>
    </footer>
    ```
