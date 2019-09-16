# blogapp
一个基于 Hexo 又添加了 hexo-theme-material(之前用的是这个) 和 hexo-theme-next(目前选择的是这个) 主题的博客框架，已经可以自行直接写日志了噢~
# 运行命令
```
# 全局安装包命令
npm install hexo-cli -g
# 装包
npm install
# 启动本地服务
hexo server
```
# 基本常用的命令
```
# 新增 .md 日志，新增之后会在 _posts 目录下自动生成一个 新的 .md 文件，和同名称的目录(放置 .md 编辑时所需要用到的静态资源)，layout 非必填项，默认使用 post 布局
hexo new [layout] 日志名称
# 本地静态资源打包
hexo g
# 清除本地打包的静态资源
hexo clean
# 部署，这个需要看官方文档 https://hexo.io/zh-cn/docs/deployment 做配置之后，才能真正的配置成功的
hexo d
```
# 资料
[hexo 官方中文文档](https://hexo.io/zh-cn/)

[我的第一篇入门笔记：Hexo 快速、简洁且高效的博客框架](http://www.soulapp.tech/2018/05/09/Hexo%20快速、简洁且高效的博客框架/)
[我的第二篇使用 hexo-theme-material 主题的笔记：Hexo 使用 hexo-theme-material 实现酷炫的页面效果](http://www.soulapp.tech/2018/05/09/Hexo%20使用%20hexo-theme-material%20实现酷炫的页面效果/)
