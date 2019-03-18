---
title: Hexo搭建个人博客教程
date: 2019-03-17 22:39:46
author: JKingKong
tags:
    - 博客
    - Hexo
    - 教程
categories: 
    - 技术
---

# Hexo搭建个人博客教程



## Hexo简介

Hexo是一款基于Node.js的静态博客框架，依赖少易于安装使用，可以方便的生成静态网页托管在GitHub和Coding上，是搭建博客的首选框架。大家可以进入hexo官网进行详细查看，因为Hexo的创建者是台湾人，对中文的支持很友好，可以选择中文进行查看。

## 系统环境

> 系统：Linux

# 教程分为四个部分

第一部分：Hexo-在本地创建博客

第二部分：部署到Github

第三部分：写博客

第四部分：使用Next主题--博客外观美化、功能拓展

## 第一部分：Hexo-在本地创建博客

> 1、安装Git
> 2、安装Node.js
> 3、安装Hexo
> 4、开始使用Hexo

### 一、在Linux上安装Git

```shell
sudo apt-get install git
git --version //查看git的版本,验证是否安装成功
```

### 二、安装Node.js

```shell
//安装node.js
sudo apt-get install nodejs
sudo apt-get install npm
```

```shell
//查看版本,验证是否安装成功
node -v
npm -v
```

### 三、安装Hexo

#### 1、安装Hexo

```shell	
npm install -g hexo-cli
```

#### 2、查看Hexo版本号,验证是否安装成功

```shell
hexo -v
```

### 四、开始使用Hexo

#### 1、在当前目录下初始化一个Hexo工程

> hexo init myblog

*注: myblog是Hexo工程的名称,可以按照自己的想法随意取*

#### 2、进入myblog文件夹

> cd myblog 

> npm install 

新建完成后，指定文件夹目录下有：
node_modules: 依赖包
**public：存放生成的页面  (使用hexo g 命令后生成的静态网页文件存放的位置)**
scaffolds：生成文章的一些模板
source：用来存放你的文章
themes：主题
**_config.yml: Hexo博客工程的配置文件**

#### 3、生成静态网页文件

> hexo g
> (完整命令： hexo generate)

```
*注:该命令必须在**Hexo工程目录**下使用,生成的静态文件保存在**myblog工程**下,的**public文件夹**里*
```

#### 4、打开Hexo服务

> hexo s
> (完整命令： hexo server)

在浏览器输入localhost:4000就可以看到你生成的博客了

## 第二部分：部署到Github

### 一、注册Github账户

[Github注册链接](https://github.com/join?source=header-home)

*如果有了就不需要注册了*

### 二、登录Github,并创建仓库

#### 1、登录

#### 2、创建仓库:**JKingKong.github.io**

![](/images/repository1.jpg)

点击**“New”**

![](/images/repository2.jpg)

![](/images/repository3.jpg)



仓库名： **你的Github用户名.github.io**

注：JKingKong----->**你的Github的用户名**

#### 3、生成SSH公钥

​	**为什么需要生成SSH公钥？**

​	大多数 Git 服务器都会选择使用 SSH 公钥来进行授权。系统中的每个用户都必须提供一个公钥用于授权，没有的话就要生成一个。

​      1、SSH 公钥默认储存在账户的主目录下的 `~/.ssh` 目录。进去看看：

```shell
$ cd ~/.ssh
$ ls
显示结果：
authorized_keys  id_rsa  id_rsa.pub  known_hosts
```

关键是看有没有用 `something` 和 `something.pub` 来命名的一对文件，这个 `something` 通常就是 `id_dsa` 或 `id_rsa`。有 `.pub` 后缀的文件就是公钥，另一个文件则是私钥。假如没有这些文件，或者干脆连 `.ssh` 目录都没有，可以用 `ssh-keygen` 来创建。该程序在 Linux/Mac 系统上由 SSH 包提供

​	2、生成SSH公钥与私钥

```shell
1、
$ git config --global user.name "yourname"
$ git config --global user.email "youremail"
2、可以用以下两条，检查一下你有没有输对
$ git config user.name
$ git config user.email
3、创建公钥与私钥,并且一路回车
$ ssh-keygen -t rsa -C "youremail"
```

​	3、查看SSH公钥

```shell
$ cat ~/.ssh/id_rsa.pub
输出：
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSU
GPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3
Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XA
t3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/En
mZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbx
NrRFi9wrf+M7Q== schacon@agadorlaptop.local
//复制上边的全部输出(你自己电脑上运行命令的全部输出结果,不是这个)
```

最后说一下SSH：

​	SSH，简单来讲，就是一个秘钥，其中，`id_rsa`是你这台电脑的私人秘钥，不能给别人看的，`id_rsa.pub`是公共秘钥，可以随便给别人看。把这个公钥放在GitHub上，这样当你链接GitHub自己的账户时，它就会根据公钥匹配你的私钥，当能够相互匹配时，才能够顺利的通过Git上传你的文件到GitHub上。

More:

[ GitHub 上有关 SSH 公钥的向导](http://github.com/guides/providing-your-ssh-key)

#### 4、在Github上添加公钥

![](/images/SSH1.jpg)

![](/images/SSH2.jpg)

![](/images/SSH3.jpg)

![](/images/SSH4.jpg)



Key框里粘贴上边**查看SSH公钥**部分所复制的东西,而后点击**“Add SSH key”**,即可完成添加公钥步骤

**使用该命令确认是否成功：**

```shell
$ ssh -T git@github.com
```

#### 5、将Hexo部署到Github

这一步，我们就可以将Hexo和GitHub关联起来，也就是将Hexo生成的静态网站部署到GitHub上

**1、打开myblog工程下的站点配置文件 `_config.yml`，翻到最后，修改**

```shell
deploy:
  type: git
  repo: git@github.com:你的Github用户名/你的Github用户名.github.io.git
  branch: master
```

保存修改。

**2、安装deploy-git**

```shell
$ npm install hexo-deployer-git --save
```

#### 6、部署

##### 1、在myblog工程下运行,以下命令

```shell
//清除缓存文件 (db.json) 和已生成的静态文件 (public)。
//在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。
$ hexo clean
//在myblog工程的public文件夹下生成静态文件
$ hexo generate
//hexo的部署命令,按照_config.yml文件里的deploy配置部署,git部署需要安装hexo-deployer-git（上边装了）,会将public文件夹下的文件部署到'你的Github用户名.github.io'仓库下
$ hexo deploy
（hexo d -g //第二、第三条命令同时执行）
```

部署完成

##### 2、访问你的静态博客网站

**https://你的Github用户名.github.io**

(记住一定要使用https)

## 第三部分：写博客

Reference:

[Hexo系列教程第三期 写作](https://www.bilibili.com/video/av39808163)

## 第四部分：使用Next主题--博客外观美化、功能拓展

### 1、从Github克隆(下载)Next主题

> git clone https://github.com/theme-next/hexo-theme-next themes/next

此命令的解释: 从Github上克隆**Next主题**到**myblog工程**下的**themes文件夹**下,并把主题命名为：**next**

### 2、在myblog工程下找到**_config.yml文件**

**_config.yml文件**(博客工程的配置文件)

### 3、打开_config.yml文件

> vim _config.yml

**注：可以使用vim命令打开,也可以用VS Code、记事本、任意文本编辑器打开**

### 4、修改配置文件,使用next主题

> 找到**theme**项,改成**theme: next**
>   而后保存

  **5、重新hexo g, hexo s**
    在浏览器输入localhost:4000,查看效果
 **注:**

- 1、‘:’后边必须有空格,yml语言格式要求
  - 2、**next**是**myblog工程**下**theme文件夹**里的**next文件夹**,即:上边从Github克隆的Next主题

#### Next主题配置参考：

(下边的教程可能使用Next版本比最新版的低一些,有些地方的配置会有不同)

[Next主题的配置-视频(强烈推荐看一下)](https://www.bilibili.com/video/av17653359/?p=1)

[Next中文使用文档-开始使用](https://theme-next.iissnan.com/getting-started.html)

[Next中文使用文档-主题配置](https://theme-next.iissnan.com/theme-settings.html)

[Next中文使用文档-第三方服务集成](https://theme-next.iissnan.com/third-party-services.html)





此篇博客参考：

[Hexo中文文档](https://hexo.io/zh-cn/docs/)

[Hexo系列教程](https://space.bilibili.com/362224537/channel/detail?cid=61636)

[hexo超完整的搭建教程，让你拥有一个专属个人博客](https://zhuanlan.zhihu.com/p/44213627)

[Next主题的配置-视频](https://www.bilibili.com/video/av17653359/?p=1)

[Next中文使用文档](https://theme-next.iissnan.com/getting-started.html)



More:

关于博客多端同步思路：

1、JKingKong.github.io仓库下 master分支保存静态网页文件

2、JKingKong.github.io仓库下 hexo分支下保存Hexo工程文件(上边的myblog文件)

3、在其它电脑使用时先克隆Hexo分支下保存Hexo工程文件,修改后生成好静态网页文件,而后推送到master分支,并且将修改好的克隆文件推送到Hexo分支

