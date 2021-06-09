---
title: mac终端实现翻墙
date: 2021-05-28 19:50:44
categories: 
- 终端
---

&emsp;&emsp;翻墙工具shadowsocks的http代理设置如下：

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210528200202.png">

&emsp;&emsp;在命令行输入以下两条指令，即可完成终端翻墙，但是每次重新启动终端的时候都需要重新输入这两条指令进行终端翻墙。

```
export http_proxy=http://127.0.0.1:1087
export https_proxy=http://127.0.0.1:1087
```

&emsp;&emsp;输入如下命令，即可得到当前自己的外网出口 IPv4 地址，就知道终端是否翻墙成功。

```
curl ip.gs
```

