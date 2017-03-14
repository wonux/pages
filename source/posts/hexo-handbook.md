---
title: Hexo搭建免费静态博客
date: 2014-11-11 11:22:22
updated: 2017-03-08 14:56:09
comments: ture
categories:
- Git
tags: 
- hexo
- pages
---

## Hexo简介

之前在Github上托管的博客就是使用jekyll搭建的，官方的Github Pages同样推荐使用它。我之前体验了一下jekyll，没有达到我想要的效果。于是寻找替代方案，搜索同类博客程序，我认识了hexo，hexo出自台湾大学生tommy351之手,是由Node.js驱动的一款快速、简单且功能强大的博客框架。Node.js是一个可以快速构建网络服务及应用的平台 。该平台的构建是基于Chrome's JavaScript runtime，也就是说，实际上它是对Google V8引擎（应用于Google Chrome浏览器)进行了封装。V8引擎执行Javascript的速度非常快，性能非常好。Node对一些特殊用例进行了优化，提供了替代的API，使得V8在非浏览器环境下运行得更好。它和jekyll相比，更快，更轻量。

[Hexo官网](https://hexo.io)

## Hexo安装

- 安装 `git`
  - Linux发行版直接使用包管理工具安装
  - Windows: [Git-Downloads](http://git-scm.com/download/)

- 安装 `node.js`
  - Gentoo package: `net-libs/nodejs`
  - Arch: `nodejs` `npm`
  - Windows: [node.js](http://nodejs.org/download/)

- 安装hexo

```cmd
npm install -g hexo-cli 
```

## 配置Hexo

- 初始化博客根目录

```cmd
hexo init blog
cd blog
```

- 安装依赖包

```cmd
npm install
```

安装之后，项目目录下出现如下文件结构：

```config
.
├── _config.yml     全局配置文件
├── package.json
├── scaffolds
├── scripts
├── source           文章存放位置
| ├── _drafts        草稿
| └── _posts         文章
└── themes
```

### 插件和主题

- plugins: 插件

添加插件的基本操作是：

```cmd
npm install <plugin-name> --save
npm update
```

然后修改blog根目录下的_config.yml，添加：

```config
plugins:
- plugin-name
```

- themes: 

安装主题：

```cmd
git clone <repository> themes/<theme-name>
```

> 无论是插件还是主题在安装后都需要在根目录下_config.yml中修改plugins和theme的值以启用他们。

~~本博客使用[pacman](https://github.com/A-limon/pacman)主题，扁平化设计，响应速快，推荐使用。修改配置参考: [http://yangjian.me/workspace/introducing-pacman-theme/](http://yangjian.me/workspace/introducing-pacman-theme/)~~

推荐Next主题：
[Next使用文档](http://theme-next.iissnan.com/)                           
[Github源码](https://github.com/iissnan/hexo-theme-next) 

### 写文章

使用Markdown语法编辑文章。使用hexo new命令生成文章或者直接在_posts目录下直接创建文件，打开后先编辑文章头部信息，如下所示是本文的头部信息，以---结尾。

```yaml
---
title: 使用Hexo搭建个人静态博客  #文章页面上的显示名称，可以任意修改，不会出现在URL中
layout: post
date: 2014-11-10 10:07:43  #文章生成时间，一般不改，当然也可以任意修改
updated: 2014-11-12 13:24
comments: true
categories: 
- Git
tags: 
- hexo
- pages
---
```

#### 文章摘要

在需要显示摘要的地方添加如下代码即可：

```
以上是摘要
<!--more-->
以下是余下全文
```

#### 文章中插入图片

使用markdown写文章，插入图片的格式为`![图片名称](链接地址)`，这里要说的是链接地址怎么写。对于hexo，使用本地路径：在/source目录下新建一个img文件夹，将图片放入该文件夹下，插入图片时链接即为/img/图片名称。

### 发布博客

这里的发布也是十分简单的，首先在github上创建名为yourname.github.io的repo，接着修改_config.yml中的deploy字段，最后执行hexo d(前提是你已经在github上添加了你本机的ssh key)，OK，现在通过yourname.github.io已经可以访问你的博客了。

> 如果是博客主页以github项目的方式创建，分支选择gh-pages。

```config
deploy:
type: git
repo: git@github.com:yourname/yourname.github.io.git
or
repo: https://github.com/yourname/yourname.github.io.git
branch: master
```

或 多个平台同时发布

```
deploy:
type: git
repo:
  github: https://github.com/yourname/yourname.github.io.git,master
  coding: https://coding.net/yourname/yourname.git,gh-pages
```

> version 3开始, type类型改为 git ，同时，需要安装 `hexo-deployer-git` 插件.

```cmd
npm install hexo-deployer-git --save
```

## Hexo使用

### init 初始化博客

```cmd
hexo init [folder]
```

如果目录不存在，将设置初始化当前目录

### new 创建新文章

```cmd
hexo new [layout] <title>
```

默认layout是post

### generate 生成静态网页文件

```cmd
hexo generate
```

### publish 发布草稿

```cmd
hexo publish [layout] <filename>
```

### server 启动本地服务

```cmd
hexo server
```

搭建本地server，进行文章预览调试。
浏览器输入http://localhost:4000 就可以看到效果。

### deploy 发布博客

```cmd
hexo deploy
```

### clean 清除缓存

```cmd
hexo clean
```

清除缓存文件：Cleans the cache file (db.json) and generated files (public).

### list 显示博客结构

```cmd
hexo list route
```

列出生成的所有博客文件路径

### 常用命令

Hexo现在支持更加简单的命令格式了，比如：

> hexo n == hexo new
> hexo g == hexo generate
> hexo p == hexo publish
> hexo s == hexo server
> hexo d == hexo deploy
> 发布博客命令：
> hexo g -d
> 或
> hexo d -g

参考：
- [hexo.io](http://hexo.io/)
- [hexo on github](https://github.com/hexojs/hexo)
- [hexo你的博客](http://ibruce.info/2013/11/22/hexo-your-blog/)

