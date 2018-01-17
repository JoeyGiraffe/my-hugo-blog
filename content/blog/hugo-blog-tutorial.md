---
author: "Hd Zhu"
title: "个人博客的搭建及部署"
date: 2017-10-10T14:20:43+08:00
slug: Hugo Blog Tutorial
draft: true
---
**首先明确下我对个人博客的需求是：**  

- [x] markdown编辑
- [x] git管理  
- [x] 独立域名

经过一番筛选，我决定选择`Hugo`作为我的博客网站生成器。
 
> *Hugo is one of the most popular open-source static site generators. With its amazing speed and flexibility, Hugo makes building websites fun again.*

### 为什么选择Hugo
- 安装非常简单，只有一个二进制文件（比如`Windows`里只是一个`hugo.exe`）；
- 生成速度快，可以将你写好的`MarkDown`格式的文章自动转换为静态的网页；
- 自带`watch`模式，页面会检测到更新并且自动刷新，极大的提高博客书写效率。

### 最终实现  

一个仓库作为代码仓库 `wercker-hugo-blog`（随意命名），管理除`public`文件夹之外的`Hugo`的全部源文件。  
一个仓库作为博客的静态页仓库，此处仓库我选择的是`gh-page`的`User`类型。每当代码仓库更新时，将自动把`public`文件夹内容（即站点的全部静态网页）`push`至`username.github.io`静态页仓库。

### 大致步骤
1. 安装`Hugo`  
2. 下载主题本地搭建博客  
3. `wercker`部署博客到`github-pages`  
4. 绑定自己的域名  

### 1. 安装Hugo

### Qulick start:

hugo -t cocoa-eh 生成你的站点静态文件，**cocoa-eh**是你使用的主题名  
hugo server -w 运行服务器，-w以监控文件的改动  
hugo new blog/hugo-blog-tutorial.md 新增一篇文章

...待续

## 推荐阅读
- [使用hugo搭建个人博客站点](https://blog.coderzh.com/2015/08/29/hugo/)
- [使用Hugo搭建个人静态博客](http://www.jianshu.com/p/bdba60260f4d)
