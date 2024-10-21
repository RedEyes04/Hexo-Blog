---
tags:
  - Hexo扩展
top_img: https://bucket.redeyes.top/2024/10/20/8c9a62.webp
categories: Hexo相关
title: "[更新ing]Obsidian+Github Action = 编写 + 自动化部署"
date: 2024-10-20T14:26:00
cover: https://bucket.redeyes.top/2024/10/20/8c9a62.webp
---
# 前言
在我们用我的这篇《最全最流畅 Hexo搭建教程「VPS」+「宝塔nignx」》我们部署完Hexo博客后我们就要开始写文章了，我们有很多种选择像VS CODE Typora Obsidian等等，但里面最舒适功能最全面的还得是我们Obsidian，但我们写完把写完的文章内容复制到Vscode里去跑一下hexo g，很是麻烦，所以我就在想有没有什么办法只要写完点击一下就能自动发布？于是就有了本期，我的方案是借助Github仓库 加上Github Action来实现
## 具体步骤如下
```
##先把VPS上/blog目录下的内容push到仓库
VPS ----> Github  (push)

##再把仓库里的内容pull到本地
Github------>Obsidian(本电脑) (pull)

 ##本地写完再Commit给Github仓库相应的Github Action检测到文件夹下有变动trigger脚本，连接到远程ssh，进行hexo g操作
 
Obsdian(本电脑)----->Github---->Github Action----> VPS（hexo g）
```