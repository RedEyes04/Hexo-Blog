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

# 服务器内容同步到Github仓库
## Github上新建仓库
首先进入Github首页新建一个仓库
![image.png](https://bucket.redeyes.top/2024/10/21/15a947.png)
## /blog下新建Git仓库
```
git init
```
![](https://bucket.redeyes.top/2024/10/21/3c7840.png)
## 创建SSH密钥
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"  ##换成你的邮箱
```
## 将公钥添加到Github
进入首页点击头像进入 “settings”
![image.png](https://bucket.redeyes.top/2024/10/21/22a197.png)
再进入SSH and GPG Keys
![image.png](https://bucket.redeyes.top/2024/10/21/97e95e.png)
把生成的公钥的内容粘贴进去保存
![image.png](https://bucket.redeyes.top/2024/10/21/ba962b.png)
## 推送目录到仓库
我们进入vs code 输入
```
git remote add origin git@github.com:yourusername/yourrepository.git
```
后面的   git@github.com:yourusername/yourrepository.git输入
![image.png](https://bucket.redeyes.top/2024/10/21/90f478.png)
SSH的地址
### 移除嵌套的 Git 仓库

```
rm -rf themes/anzhiyu/.git
```
### 添加到暂存区

```
git add .
```
### 新建仓库用户
```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

### 设置上游分区master并推送
```
git push --set-upstream origin master
```

我们再打开Github相应的仓库界面，就能发现已经全部同步过去了
![image.png](https://bucket.redeyes.top/2024/10/21/58185c.png)
## 拉取文件到本地Obsidian
