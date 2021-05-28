---
title: PicGo + Gitee(码云)实现markdown图床
date: 2021-05-28 20:45:44
categories: 
- Hexo博客
---

# 图床介绍

&emsp;&emsp;咱们写博客的时候，总是需要插入图片的，图片存在本地上传到博客网站就没法显示了。

&emsp;&emsp;图床是干什么的？

&emsp;&emsp;图床就是一个便于在博客中插入在线图片链接的个人图片仓库。设置图床之后，在自己博客中插入的图片链接就可以随时随地在线预览了，并且不会因为任何意外原因无法查看，除非自己亲自删除。

&emsp;&emsp;神奇的PicGo就是为了解决这个问题诞生的，它可以将图片上传到指定的图床上，然后返回markdown链接，直接粘贴到你的文档中。

# 码云

&emsp;&emsp;码云上新建仓库

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210528211322.png" width="50%" height="50%" title="码云新建仓库">

&emsp;&emsp;点击头像，进入设置

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210528211756.png" width="50%" height="50%" title="码云新建仓库">

&emsp;&emsp;私人令牌 -> 生成新令牌

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210528224958.png" title="令牌">

&emsp;&emsp;把projects这一项勾上，其他的不用勾，然后提交,就会生成一串数字，这一串数字就是你的token

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210528225700.png" title="token">

# PicGo

&emsp;&emsp;进入[picgo官网](https://github.com/Molunerfinn/PicGo)进行下载安装。安装之后打开主界面，选择最底下的插件设置，搜索gitee，点击右边的gitee-uploader 1.1.2开始安装。

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210528230049.png" title="插件设置">

&emsp;&emsp;配置PicGo

&emsp;&emsp;repo：用户名/仓库名称，找不到的可以直接复制仓库的url

&emsp;&emsp;branch：分支，这里写上master

&emsp;&emsp;token：填入上面码云生成的私人令牌

&emsp;&emsp;path：路径，一般写上img

&emsp;&emsp;customPath：提交消息，这一项和下一项customURL都不用填。

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210528230716.png" title="gitee设置">

# 图片上传

&emsp;&emsp;在此处放入图片，即可生成markdown形式的url

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210528231052.png" title="图片上传">
