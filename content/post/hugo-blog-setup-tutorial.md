---
title: "Hugo + Github Pages + Wercker搭建博客"  
slug: hugo-blog-setup-tutorial  
metaAlignment: center  
coverMeta: out  
date: 2017-10-10  
categories:
- tutorial
tags:
- hugo
- github pages
- wercker  

showSocial: false  

---

使用`Hugo`生成静态博客托管于`GitHub Pages`之上，并利用`Wercker`实现自动部署。
<!--more-->

<!--toc-->

## Hugo介绍
> Hugo is one of the most popular open-source static site generators. With its amazing speed and flexibility, Hugo makes building websites fun again.

完全满足我对个人博客的需求：

- [x] markdown编辑
- [x] git管理
- [x] 独立域名  
并且自带调试模式，本地编辑博文时{{< hl-text cyan >}}页面会检测到更新并且自动刷新{{< /hl-text >}}，极大的提高书写效率。

## Hugo安装
Hugo的安装非常简单，可参考【[官网教程](https://gohugo.io/getting-started/installing/)】。安装完成后将其加入环境变量，编辑—>变量名Path，在原变量值的最后面加上`D:\Environment\Hugo;`即你下载的`hugo.exe`所在目录路径。

## Theme下载
    hugo new site my-hugo-blog #新建站点
    cd my-hugo-blog/themes
    git clone https://github.com/kakawait/hugo-tranquilpeak-theme.git #下载主题
## Wercker部署

新建仓库`my-hugo-blog`作为代码仓库，管理`Hugo`的全部源文件。新建仓库`username.github.io`作为博客的静态页仓库（username替换为自己的github用户名）。  
工程根目录下创建`wercker.yml`，下面是我的配置可参考，注意把domain， repo替换成自己的域名及仓库名。
{{< codeblock "wercker.yml" "go" "https://github.com/JoeyGiraffe/my-hugo-blog/blob/master/wercker.yml" "wercker.yml" >}}
# This references a standard debian container from the
# Docker Hub https://registry.hub.docker.com/_/debian/
# Read more about containers on our dev center
# http://devcenter.wercker.com/docs/containers/index.html
box: debian
# You can also use services such as databases. Read more on our dev center:
# http://devcenter.wercker.com/docs/services/index.html
# services:
    # - postgres
    # http://devcenter.wercker.com/docs/services/postgresql.html
    
    # - mongo
    # http://devcenter.wercker.com/docs/services/mongodb.html

# This is the build pipeline. Pipelines are the core of wercker
# Read more about pipelines on our dev center
# http://devcenter.wercker.com/docs/pipelines/index.html
build:
    # Steps make up the actions in your pipeline
    # Read more about steps on our dev center:
    # http://devcenter.wercker.com/docs/steps/index.html
    steps:
        - script:
            name: install git
            code: |
                apt-get update
                apt-get install git -y
        - script:
            # 如果使用submodules, 记得添加配置文件.gitmodules
            name: initialize and update git submodules
            code: |
                git submodule init
                git submodule update --remote --recursive
        - arjen/hugo-build@2.8.0:
            # your hugo theme name
            theme: hugo-tranquilpeak-theme
            flags: --buildDrafts=false
deploy:
    steps:
        - install-packages:
            packages: git ssh-client
        # 官方给的lukevivier/gh-pages@0.2.1会部署到gh-pages分支，17年我用的时候没这毛病，这里改用别的Step
        # 部署public目录下的静态文件至username.github.io的master分支
        - sf-zhou/gh-pages@0.2.6:
            token: $GIT_TOKEN
            domain: handsomezhu.me
            repo: JoeyGiraffe/joeygiraffe.github.io
            branch: master
            basedir: public
{{< /codeblock >}}

官网对于`Wercker`的配置还是老版本的【[教程](https://gohugo.io/hosting-and-deployment/deployment-with-wercker#set-up-wercker)】。根据老版教程创建完应用之后，默认只有一个`build`，点击 `Add new pipeline`，添加`deploy pipeline`
![](/images/hugo-blog-setup-tutorial/add-deploy-pipeline.png)

为当前的`pipeline`设置环境变量，`Key`与`wercker.yml`中对应`pipeline`下的变量名保持一致，并生成 [GIT_TOKEN](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) 填入`Value`。
![](/images/hugo-blog-setup-tutorial/add-git-token.png)

设置`Workflows`，添加刚新增的`deploy pipeline`即可。
![](/images/hugo-blog-setup-tutorial/edit-workflows-first.png)  
![](/images/hugo-blog-setup-tutorial/edit-workflows-second.png)

此后，每当代码仓库更新时，`Wercker`会自动生成博客静态页并提交至静态页仓库。  

## Domain解析
添加两条记录类型为`CNAME`的解析，一条主机记录为`@`，一条主机记录为`www`，记录值格式都为你的`username.github.io`，如下：

| 类型  | 名称 |         值         |
| :---: | :--: | :----------------: |
| CNAME |  @   | username.github.io |
| CNAME | www  | username.github.io |

{{< alert warning >}}
GoDaddy不支持CNAME的@解析，改为添加A类型的@记录，`ping username.github.io`
{{< /alert >}}

THE END.







