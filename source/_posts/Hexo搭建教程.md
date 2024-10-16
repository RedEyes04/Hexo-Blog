---
title: "[更新ing]Hexo搭建教程「VPS」+「宝塔nignx」"
date:
  "{ date }": 
tags:
  - HEXO
top_img: https://bucket.redeyes.top/2024/10/16/670fb5395bd2a.webp
categories: Hexo相关
cover: https://bucket.redeyes.top/2024/10/16/670fb5395bd2a.webp
---
## 前言
本篇文章将会教你从头开始教你一种，目前网络上最流畅、最快的hexo部署在vps服务器的方案！




# 服务器相关
## 服务器选择
这里推荐大家去用阿里云的~~飞天计划给的服务器~~，（飞天计划貌似已经被取消了，之后[天工开物](https://university.aliyun.com/)计划还在）有七个月，最后如果符合在校或者在教育机构工作的话，天工开物还能获得300元的无门槛券，能续上三个月，一共加起来就是十个月，这里给大家 飞天计划的链接大家，完成一些相应的操作就行了，很简单，这里不过多赘述
## 服务器的配置
在有了服务器之后，我们需要重新安装一次系统，这里推荐用debian12的系统，然后我们需要一款shell工具，我用的多的是[xshell](https://www.xshell.com/zh/xshell-download/)，可以去官下到然后免费使用，填写外网ip地址和密码即可连接使用
## 宝塔面板安装
这里为了方便大家使用，可以选择一款面板来辅助我们操作服务器，进入官网然后复制debian的安装连接，直接复制到xhell里安装就好了
记住外网的访问连接，输入 bt 6 / bt 5分别修改用户名，然后进去面板安装环境

# 域名相关
## 顶级域名购买
域名购买的渠道很多，我这里用的阿里云，第一年好像就9元，之后都是三十几一年，还是很便宜的，不过我们用的国内服务器，是需要进行备案的，这里只有一个地方要说一下，阿里云里备案是要一个备案码的，你可以去官方买一个99元/个，如果觉得贵的话也可以到一些小程序去买，像 备案狗十块左右就能买到了！
## 二级域名
这类域名网上一招一大堆，就能获得，但一般长得不好看，这里不做推荐，有需要的可以自行百度和B站就能找到

## 域名解析
有了域名之后我们可以去相应的域名解析页面常用的记录类型有三种
- A记录
	A记录一般直接指向服务器的外网IP地址
- CNAME
	一般用于验证域名所有权以及进行相应的CDN加速服务
- TXT
	也是一种多用语验证域名所有权的常见方法
这里我们现先加A记录的解析，到自己的服务器外网IP地，在添加自己想要的主机记录，博客的话一般是www或者blog。
## 添加网站
到宝塔面板里添加网站，因为hexo是静态网站，所以下面我们不要勾选PHP版本，也不要建立相应的数据库，然后输入刚刚添加的网站记录
## SSL证书申请
接着我们要申请相应网站的SSL证书，直接选择上面的 「Let's Encrypt」 只要前面一步正确进行了DNS解析就会成功获得相应的证书，点击保存，开启强制https。接着就可以访问页面了！

# HEXO安装
## nodejs安装
首先根据官网给的文章，安装hexo之前要先安装nodejs，现进入nodejs的官网，点击【】下载，然后我们使用xshell里的xftp工具传上去，接着我们输入
```
tar
```
进行解压，接着我们给解压完的文件夹换个名字
```
mv
```
然后我们也还可以把原压缩包删除
```
rm -f 
```
接着设置软链接，注意这里的地址根据你的实际地址来定，我的是放在root目录，也就是（~）/「nodejs」 这样的root目录在整个目录的位置是这样的/root/「nodejs」或者~/nodejs
```
ln -s ~/nodejs/bin/node /usr/local/bin/
```
```
ln -s ~/nodejs/bin/npm /usr/local/bin/
```
接着我们来验证一下是否安装成功
分别输入
```
node -v
```

```
npm -v
```
如果能出现版本号那就是安装成功了

## 安装hexo脚手架
```
npm install hexo-cli -g
```

安装完为了方便使用，我们给hexo也做个软链接，方法和上面一样
```
ln -s ~/nodejs/bin/hexo /usr/local/bin/
```


同样的，我们软链接完可以用这个命令看一下是否正确进行了软链接
```
hexo -v
```

## 初始化hexo内容

接着我们到根目录（不是root目录），root的上一层目录，我们新建新的文件夹
```
mkdir blog
```
进入文件夹
```
cd blog
```
初始化内容
```
hexo init
```
稍等片刻后我们便能得到初始化的内容

# VS Code 软件的安装和使用（如果已经会使用的可以跳过哦！）
接下来我们会进行配置主题文件，如果我们使用xshell和xftp会不太方便，所以我们这里可以使用一款超级好用的软件！Vscode 我们直接进入[官网](https://code.visualstudio.com/)进行下载和安装！
安装完进去后，我们点击右边的插件选项，搜索Chinese ，进行安装汉化
安装完右下角会让你重启软件，重启完就汉化好了！
## ssh🔗连接服务器
我们点击左下角的，打开远程窗口，进行然后在上面输入相应的内容
```
ssh root@[你的IP地址]
```
输入完密码后会让你写入文件里，然后我们就成功连接上服务器了，但是你发现每次打开文件夹的时候都会让我们再次输入密码，很不方便，所以我们这里还要再配置以下免密ssh链接






## 应用主题
# 配置主题
## 安装anzhiyu主题

```
git clone -b main https://github.com/anzhiyu-c/hexo-theme-anzhiyu.git themes/anzhiyu
```

## 安装渲染插件

```
npm install hexo-renderer-pug hexo-renderer-stylus --save
```

## 优化覆盖配置

```
cp -rf ./themes/anzhiyu/_config.yml ./_config.anzhiyu.yml
```
我们安装完可以在theme文件夹里找到anzhiyu的主题文件，里面有个_config.yml，但是我们每次用命令更新完的时候，原有的配置文件会被覆盖掉，会有点麻烦，每次更新的时候要先复制一份，上面的代码是把_config.yml这个文件复制到/blog根目录，复制到根目录的文件优先级会比里面的优先级高，所有我们之后改一些配置直接改_config.anzhiyu.yml，就行了！


接着我们在根目录找到文件_config.yml,往下翻,把theme改成anzhiyu
找到
```
theme: anzhiyu
```

## Hexo命令简单学习
```
hexo g   ##根据_config.anzhiyu.yml的内容生成静态文件在根目录的public文件夹下
hexo cl  ##清除public下所有文件夹
hexo d   ##推送到远程仓库（我们这种方法用不到）
hexo s   ##在服务器的4000端口开启服务器进程，可以进行访问
```


### 简单尝试
我们可以在根_config.yml里面配置配置一些相关内容，然后服务器的本地端口开启hexo服务，以下是我的配置文件，我也会在后面写上相应注释，各位跟着后面改就行了

```
# Hexo Configuration

## Docs: https://hexo.io/docs/configuration.html

## Source: https://github.com/hexojs/hexo/

  

# Site

title: REDEYESの小窝        ##浏览器导航栏显示的标题

subtitle: '纵有疾风起，人生不言弃！'      ##浏览器导航栏显示的副标题

description: 'REDEYES的博客'       ##博客的描述

keywords:                  ##博客的关键词
 
author: REDEYES             ##博客的作者，会影响到anzhiyu主题里作者的名字

language: zh-CN          ##语言的设置  zh-CN为中文 

timezone: ''            ##时区一般不要设置

  

# URL

## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'

url: https://www.redeyes.top       ##博客的地址    下面就没什么要设置的了，现设置到这把！

permalink: :year/:month/:day/:title/

permalink_defaults:

pretty_urls:

  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks

  trailing_html: true # Set to false to remove trailing '.html' from permalinks

  

# Directory

source_dir: source

public_dir: public

tag_dir: tags

archive_dir: archives

category_dir: categories

code_dir: downloads/code

i18n_dir: :lang

skip_render:

  

# Writing

new_post_name: :title.md # File name of new posts

default_layout: post

titlecase: false # Transform title into titlecase

external_link:

  enable: true # Open external links in new tab

  field: site # Apply to the whole site

  exclude: ''

filename_case: 0

render_drafts: false

post_asset_folder: false

relative_link: false

future: true

syntax_highlighter: highlight.js

highlight:

  enable: true

  line_number: true # <- 改这里

  auto_detect: true

  tab_replace:

  wrap: true

  hljs: false

prismjs:

  preprocess: true

  line_number: true

  tab_replace: ''

  
  

# Home page setting

# path: Root path for your blogs index page. (default = '')

# per_page: Posts displayed per page. (0 = disable pagination)

# order_by: Posts order. (Order by date descending by default)

index_generator:

  path: ''

  per_page: 10

  order_by: -date

  

# Category & Tag

default_category: uncategorized

category_map:

tag_map:

  

# Metadata elements

## https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta

meta_generator: true

  

# Date / Time format

## Hexo uses Moment.js to parse and display date

## You can customize the date format as defined in

## http://momentjs.com/docs/#/displaying/format/

date_format: YYYY-MM-DD

time_format: HH:mm:ss

## updated_option supports 'mtime', 'date', 'empty'

updated_option: 'mtime'

  

# Pagination

## Set per_page to 0 to disable pagination

per_page: 10

pagination_dir: page

  

# Include / Exclude file(s)

## include:/exclude: options only apply to the 'source/' folder

include:

exclude:

ignore:

  

# Extensions

## Plugins: https://hexo.io/plugins/

## Themes: https://hexo.io/themes/

theme: anzhiyu

  
  

# Deployment

## Docs: https://hexo.io/docs/one-command-deployment

deploy:

  type: ''
```

接着我们设置完，我们可以

```
hexo cl 
```
```
hexo g
```
```
hexo s
```
hexo 三连打开服务器


# 仍在努力更新中！！