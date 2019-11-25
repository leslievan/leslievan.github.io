---
title: "【教程】加速apt（apt-get速度慢）"
tags: [ "Linux", "Ubuntu", "Software" ]
categories: [ "Tutorial" ]
date: 2019-03-24 16:05:36
keywords: ["Ubuntu","apt","镜像"]

---

![](https://leslie-cloud.oss-cn-beijing.aliyuncs.com/2019/03/2019-03-24-8376b517-0.jpg)

使用OPSX镜像站为APT进行加速。

<!--more-->



Ubuntu默认使用其[Main Server](archive.ubuntu.com)作为默认下载源，由于这个下载源在国外，国内访问源的速度会非常地慢（可能只有几KB到几十KB），庆幸的是，许多高校和公司为此建立了一些镜像站，诸如阿里巴巴开源镜像站[OPSX](https://opsx.alibaba.com)、[清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn)，这些镜像站的存在让我可以更方便、更快速地获取各种开源软件（包括但不限于Linux在内的一系列系统/应用软件）。

这里说明三种更改默认下载源的方法。

## 命令行配置

> 新手推荐使用([图形界面配置](#图形界面配置)）

一般情况下，将`/etc/apt/sources.list`文件中Ubuntu默认的源地址`http://archive.ubuntu.com/`替换为镜像的地址即可。

```bash
# 这里以清华镜像为例
# Ubuntu 1604
$ sudo rm /etc/apt/sources.list && sudo wget https://tinyurl.com/y28j6bh6 -O /etc/apt/sources.list && sudo apt-get update
# Ubuntu 1804
$ sudo rm /etc/apt/sources.list && sudo wget https://tinyurl.com/y28j6bh6 -O /etc/apt/sources.list && sudo apt-get update

# 清华tuna协会也推出了“Oh-My-TUNA”脚本，具体的可以看最后一节
$ wget https://tuna.moe/oh-my-tuna/oh-my-tuna.py
# For yourself
$ python oh-my-tuna.py
# ...or for everyone!
sudo python oh-my-tuna.py --global
```

这将解决由于下载服务器在国外而导致的速度过慢以至于无法下载的问题。

## 图形界面配置

图形界面操作为：`Software & Update`->`Download from`，选择`China`下的`mirrors.aliyun.com`。

> Bilibili：https://www.bilibili.com/video/av47223665/ 

<iframe width='100%' height=500px src="//player.bilibili.com/player.html?aid=47223665&cid=82702213&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
## “一键使用TUNA”

> 清华大学 TUNA 协会，全名清华大学学生网络与开源软件协会，是由清华大学热爱网络技术和开源软件的极客组成的学生技术社团。

清华开源软件镜像站由TUNA协会运行维护，为了方便用户使用他们推出了“一键使用TUNA”的服务，具体操作及介绍，请直接查看其项目主页，这里不越俎代庖。

oh-my-tuna介绍：<https://mirrors.tuna.tsinghua.edu.cn/news/#oh-my-tuna>

oh-my-tuan主页：<https://tuna.moe/oh-my-tuna/>
