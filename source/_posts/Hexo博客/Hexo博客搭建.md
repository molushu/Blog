---
title: Hexo博客搭建
date: 2021-05-27 13:23:44
categories: 
- Hexo博客
---

# 安装Node.js

&emsp;&emsp;[官网](https://nodejs.org/en/)下载并安装。

&emsp;&emsp;打开终端，输入如下命令，并输入密码，切换到root用户。

```
sudo su
```

&emsp;&emsp;终端输入如下命令即可看到安装的版本。

```
node -v
npm -v
```

# 安装Hexo框架

&emsp;&emsp;npm是包管理器，输入如下命令，利用npm安装cnpm

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

&emsp;&emsp;输入如下命令安装Hexo框架

```
cnpm install -g hexo-cli
```

# 本地博客搭建

&emsp;&emsp;本地新建一个名为Blog的文件夹，并终端进入Blog文件夹路径，输入如下命令进行初始化，即可在Blog文件夹中生成初始文件。

```
hexo init
```

&emsp;&emsp;输入如下命令，启动博客，即可在本地[http://localhost:4000](http://localhost:4000)网址看到博客

```
hexo s
```

&emsp;&emsp;在Blog/source/_posts文件夹下新建md博客文档，编写博客。博客编写完毕后，先输入hexo clean进行清理，再输入hexo g进行生成，最后输入hexo s，即可在本地[http://localhost:4000](http://localhost:4000)看到新建的博客文章。

```
hexo clean
hexo g
hexo s
```

# 与远端github连接

&emsp;&emsp;在github上新建一个仓库，名字必须为:用户名.github.io

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210527162705.png" width="50%" height="50%" title="github博客仓库">

&emsp;&emsp;输入如下命令，安装git的部署插件

```
cnpm install --save hexo-deployer-git
```

&emsp;&emsp;打开Blog/_config.yml文件，修改文件最底端代码

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210527163626.png" title="博客配置">

&emsp;&emsp;输入如下命令，即可将本地博客部署到github远端。此时在[https://molushu.github.io/](https://molushu.github.io/)网址即可访问博客。

```
hexo d
```

# 更换博客主题(Next)

&emsp;&emsp;输入如下命令，即可在Blog/themes文件夹下生成next主题文件夹

```
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

&emsp;&emsp;打开Blog/_config.yml文件，将主题修改为next主题

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210527231558.png" title="博客配置">

&emsp;&emsp;依次输入以下命令，即可在远端看到更换主题后的博客

```
hexo clean
hexo g
hexo d
```

# Next主题下配置分类

&emsp;&emsp;打开Blog/themes/next/_config.yml文件，放开categories: /categories/ || fa fa-th这行代码

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210527233159.png" title="博客配置">

&emsp;&emsp;终端输入如下命令，即可在Blog/source文件夹下生成categories文件夹

```
hexo new page categories
```

&emsp;&emsp;打开Blog/source/categories/index.md文件，添加上type: "categories"这段代码就能让主题识别该页面为分类页面了

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210527234350.png" title="博客配置">

# 给博客文章设置分类属性

&emsp;&emsp;打开需要添加分类的文章，如下表示将这篇文章添加到Hexo博客这个分类当中

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210527234841.png" title="博客配置">

&emsp;&emsp;&emsp;打开需要添加分类的文章，如下表示将这篇文章添加到Hexo博客/Hexo博客2这个二级分类当中

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210527235054.png" title="博客配置">

# Next主题添加Valine评论系统

&emsp;&emsp;因为 Valine 是基于 LeanCloud 系统的，所以先在 [LeanCloud](https://console.leancloud.cn/apps) 中注册账号。注册登陆后，访问控制台，创建应用，选择开发版，创建好之后就生成了 App ID 和 App Key。然后在Blog/themes/next/_config.yml文件中修改关于 Valine 的配置。

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210527235703.png" title="博客配置">

