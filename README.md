# swim2moon.github.io
:clock1030: username.github.io

1. [绑定自己的域名到GitHub-Pages](https://www.zhihu.com/question/31377141)
2. [安装hugo](https://gohugo.io/getting-started/installing)

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

Todos:
----写博文----
phpstorm常用配置项
homestead环境搭建及phpredis安装
