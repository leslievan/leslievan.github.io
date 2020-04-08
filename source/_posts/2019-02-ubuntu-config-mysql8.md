---
title: "【教程】Ubuntu配置MySQL 8.0"
date: 2019-02-07 15:59:14
tags: [ "Linux", "Ubuntu", "Software" ]
categories: [ "Tutorial" ]
keywords: ["mysql", "ubuntu"]

---

翻译自官方教程：https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/
<!--more-->



# 系统环境及配置

> Ubuntu 18.04
>
> MySQL 8.0

# 下载安装MySQL拓展包

> [官方最新下载地址](https://dev.mysql.com/downloads/repo/apt/)
>
> [百度云下载地址](https://pan.baidu.com/s/1OaHHJ_1DLUQVe0VdHQ91DA)（提取码：9mmz，MD5: `65b0b081ce9cf90c7e2d3cc540aa8955`）
>
> 建议使用官方最新下载地址

1. 下载后得到类似于`mysql-apt-config_0.x.x-x_all.deb`的安装包，打开终端，输入命令定位到安装包所在位置，并安装

    ```shell
    $ sudo dpkg -i /PATH/mysql-apt-config_0.x.x-x_all
    ```

    将`mysql-apt-config_0.x.x-x_all.deb`置换为你所下载的文件名。

2. 安装过程中将对`mysql-apt-config`进行配置，选择你所需要的MySQL版本，百度云提供的安装包默认版本为`mysql-8.0`，配置过程如下图所示，配置结束后选择`Ok`。
    ![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/02/2019-02-07-Ubuntu%E9%85%8D%E7%BD%AEMySQL8-1.png)

3. 打开终端，输入以下命令更新软件仓库：

    ```shell
    $ sudo apt-get update
    ```

# 使用APT安装MySQL

使用如下命令安装MySQL：

```shell
sudo apt-get install mysql-server
```

这条命令将会同时安装`mysql-client`和`mysql-common`。

下载完安装包后将会提醒你配置**根用户密码（root password）**，请牢记该密码。