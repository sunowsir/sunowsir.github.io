---
title: hexo低成本搭建静态网页博客
date: 2019-09-16 12:01:15
tags: note
cover: title.jpg
---





## 引言
好多同学有写博客的习惯，也有各大例如csd*、简*等博客平台。
但是这些平台毕竟是盈利平台，无法做到对自己的博客完全掌控，有一丝丝的不爽快。想要DIY一下几乎不可能。在这里推荐同学们自己动手丰衣足食。
## 准备知识
1. github最基本的使用（拥有账号，会建立仓库，与本地电脑进行远程代码推送）。
2. git最基本的使用（推送代码到远程例如github这种托管平台）。
3. linux最基本的常用的命令（推荐linux平台）。
## 原理解析
* 托管与访问
  github为每一个用户提供了免费的500M（貌似是）的空间，建立名称为`username.github.io`的仓库，可以把我们做好的博客静态网页放到该仓库中，然后使用`username.github.io`就可以访问我们的博客了。
* 博客代码生成
  使用hexo可以一行命令轻松生成可以高度定制的现成的博客代码，hexo官网还提供了大量的插件和主题供使用者DIY。
## 搭建步骤
> 此处忽略本地git与github绑定相关知识以及代码推送相关知识。
> 这里本机环境使用linux（debian系）
1. 在github平台上登录账号，新建名称为`username.github.io`的仓库备用。例如`sunowsir.github.io`（username是github用户名）
2. 安装nodejs与npm环境（自行百度），确保`npm -v`正常显示。
3. 安装hexo：`sudo npm install -g hexo-cli。
4. 新建一个hexo项目：`hexo init 项目名称`。例如`hexo init MYclub`。
5. 进入项目目录：`cd MYclub`。
6. 创建新文章：`hexo new 文章标题`，生成一个markdown文件，在`source/_posts/`下。
7. 配置文件：_config.yml
8. 生成博客代码：`hexo g`，生成的博客代码在项目目录下的public目录中。
9. 将public中所有的内容都push到之前创建的仓库中。
10. 打开浏览器访问`username.github.io`看看。



## 经验
- npm报错
  错误提示
  ```bash
  npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.0.7: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
  ```
  解决方案
  ```bash
  # 在博客根目录下
  npm i -f
  ```
- 无法使用`hexo d`部署
  1. _config.yml文件中，找到如下内容，替换`yourname`为你的github的名字，
  ```bash
  deploy:
  type: git
  repo: https://github.com/yourname/yourname.github.io.git
  branch: master
  message: 推送原因（例如：update some page ）
  ```
  2. 执行`npm install`，安装缺少的模块
  3. 执行`npm clean`，清理缓存
  4. 执行`hexo g`，重新构建
  5. 执行`hexo d`，部署
- markdown无序列表渲染异常
　https://github.com/viosey/hexo-theme-material/issues/588

  



---
[更多hexo相关参考](https://hexo.io/zh-cn/docs/)：https://hexo.io/zh-cn/docs/
