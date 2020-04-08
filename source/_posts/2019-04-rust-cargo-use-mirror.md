---
title: "【教程】安装&加速Rust"
tags: [ "Rust", "tool", "Linux" ]
categories: [ "Tutorial" ]
date: 2019-04-04 18:13:19
keywords: ["rust", "Linux"]
---

和`apt`、`pip`等一样，`Rust`的源同样也在国外，被GFW拒之门外，速度实在难以言表，这里介绍安装过程以及如何使用中科大的源为`Rust`和`Cargo`加速。

<!--more-->

# 安装

## Ubuntu源

`rustc`是Rust的软件包，默认已被收录，如果不需求最新版本，可以直接使用`apt`进行安装，前面已经有一篇文章介绍了[如何加速apt](/2019/03/apt-use-mirror/)：

```shell
sudo apt-get install rustc cargo
```

## Rustup

在终端里面输入：

```shell
curl https://sh.rustup.rs -sSf | sh
```

之后跟随提示所有选项选择默认即可。

# 使用中科大源进行加速

在`~/.cargo/config`添加以下内容：

```conf
[registry]
index = "git://mirrors.ustc.edu.cn/crates.io-index"
```

如果所处的环境中不允许使用 git 协议, 可以把上述地址改为

```conf
index = "http://mirrors.ustc.edu.cn/crates.io-index"
```

如果 cargo 版本为 0.13.0 或以上, 需要更改`~/.cargo/config`为以下内容：

```conf
[source.crates-io]
registry = "https://github.com/rust-lang/crates.io-index"
replace-with = 'ustc'
[source.ustc]
registry = "git://mirrors.ustc.edu.cn/crates.io-index"
```

