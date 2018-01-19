# swim2moon.github.io
:clock1030: username.github.io


新建站点 blog为你的站点目录 `cd Sites hugo new site blog`
下载主题到themes目录下
` cd blog
git clone https://github.com/nishanths/cocoa-hugo-theme.git themes/cocoa
`
可使用主题的exampleSite
站点根目录执行hugo server命令 -w监听
config修改则需要重启

layouts & static 直接覆盖


发表一片文章
hugo new blog/your-new-post.md


```
slug url文件路径
heading title

```

然后hugo会自动生成这样一个目录结构：

  ▸ archetypes/
  ▸ content/
  ▸ layouts/
  ▸ static/
    config.toml
简要介绍一下，config.toml是网站的配置文件。content目录里放的是你写的markdown文章，layouts目录里放的是网站的模板文件，static目录里放的是一些图片、css、js等资源。

Quick Start
hugo -t cocoa-eh 生成你的站点静态文件，**cocoa-eh**是你使用的主题名  
hugo server -w 运行服务器，-w以监控文件的改动  
hugo new blog/hugo-blog-tutorial.md 新增一篇文章


Todos:
----写博文----
phpstorm常用配置项
homestead环境搭建及phpredis安装
