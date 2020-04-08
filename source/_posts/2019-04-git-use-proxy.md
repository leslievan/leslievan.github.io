---
title: "【教程】加速git（push/clone速度慢）"
tags: [ "Git", "Software" ]
categories: [ "教程" ]
date: 2019-04-04 14:22:33
keywords: ["git", "proxy"]
---

作为一名CS专业的学生，我们大部分时候都在和代码打交道，那么就不得不知道`git`和[`GitHub`](https://github.com)了，`git`最基本的命令就是使用`git clone`从代码托管平台下载代码以及使用`git push`将本地更改推送到远程仓库，然而由于众所周知的原因，世界上最大的代码托管平台`GitHub`在国内访问的速度实在堪忧，这里提供一些网络加速的方法。

<!--more-->



# 为git使用代理

如果你已经拥有了一些代理软件，那么直接为`git`设置代理是最好的提速方法，这里以`ss`为例，假设本地代理地址为`127.0.0.1：1080`，那么你可以使用以下命令为`git`设置代理：

```shell
# http options
git config --global http.proxy "socks5h://127.0.0.1:1080"
# unknown section name
git config --global https.proxy "socks5h://127.0.0.1:1080"

# 查看更改是否成功
git config --global --get http.proxy
git config --global --get https.proxys

# 取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy
```

这一方法可以加速克隆使用http/https协议进行传输的仓库，使用ssh协议的需要其他设置，这里不加以阐述。

```shell
# http/https协议
git clone https://github.com/leslievan/verilog.git
# ssh协议
git clone git@github.com:leslievan/verilog,git
```

# 修改host文件

在`git clone`或`git push`时，实际上并不是直接向`github.com`发送请求，而是对`github.global.ssl.fastly.net`发送请求与通信，Fastly公司在中国有着众多的CDN节点，GitHub可能因为成本或者其他原因，并没有在中国搭设自己专属的CDN节点，我们可以通过修改`host`文件来加速对这个域名的访问。

```conf
# windows下修改C:\Windows\System32\drivers\etc\hosts
# Linux/Mac下修改/etc/hosts
# 在最后加上

151.101.77.194  github.global.ssl.fastly.net
13.229.188.59   github.com
185.199.109.153 assets-cdn.github.com
151.101.76.249  global-ssl.fastly.net
```

然后刷新DNS缓存。

```conf
# windows
ipconfig /flushdns
# linux/mac
sudo /etc/init.d/network-manager restart
```

如果网络没问题的话，修改后的速度一般都能达到`MB/s`的级别。

# git shallow clone

`git clone`默认是将整个项目全须全尾地下载到本地，实际上我们大部分时候都只是想要最新的版本，下载整个项目是无用的且花费较大的，这时候我们可以使用：

```shell
git clone --depth=1 https://github.com/leslievan/verilog.git
```

其中，`--depth=1`代表最新的版本，通过这一参数的限定可以大大减少下载的数据量，如果你的网速较慢且无法改变，无法开源那么不妨尝试节流。