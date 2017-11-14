---
author: "Hd Zhu"
title: "个人博客的搭建及部署"
date: 2017-10-10T14:20:43+08:00
slug: Hugo Blog Tutorial
draft: true
---
> Hugo is one of the most popular open-source static site generators. With its amazing speed and flexibility, Hugo makes building websites fun again.

## 为什么选择Hugo
- 安装非常简单，只有一个二进制文件（比如Windows里只是一个hugo.exe）；
- 生成速度快，可以将你写好的MarkDown格式的文章自动转换为静态的网页；
- 自带watch模式，页面会检测到更新并且自动刷新，极大的提高博客书写效率。

## 最终实现  
代码仓库 wercker-hugo-blog（随意命名），管理除public文件夹之外的全部源文件。连接代码仓库到Wercker，每次代码仓库更新将自动把public文件夹内容（即站点的全部静态网页）push至博客仓库 username.github.io，这里我选择的是把博客托管于gh-page的User类型。

大致步骤  
1. 安装Hugo  
2. 下载主题本地搭建博客  
3. wercker部署博客到github-pages  
4. 绑定自己的域名  

## 安装Hugo

### Qulick start:

hugo -t cocoa-eh 生成你的站点静态文件，**cocoa-eh**是你使用的主题名  
hugo server -w 运行服务器，-w以监控文件的改动  
hugo new blog/hugo-blog-tutorial.md 新增一篇文章

...待续

## 推荐阅读
- [使用hugo搭建个人博客站点](https://blog.coderzh.com/2015/08/29/hugo/)
- [使用Hugo搭建个人静态博客](http://www.jianshu.com/p/bdba60260f4d)
