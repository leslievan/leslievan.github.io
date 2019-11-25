---
title: "【教程】Ubuntu配置VMware Workstation"
tags: [ "Linux", "Ubuntu", "Software", "VMware" ]
date: 2019-02-02 14:31:36
categories: [ "Tutorial" ]
keywords: ["vmware", "虚拟机"]

---

VMware Workstation是VMware公司推出的一款桌面虚拟计算软件，具有Windows、Linux 版本。此软件可以提供虚拟机功能，使计算机可以同时运行多个不同操作系统。
<!--more-->



# 系统环境

> Ubuntu 18.04
>
> [VMware Workstation 15](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html "VMware官方下载地址")

# 安装VMware Workstation

## 定位到安装包所在文件夹

```shell
$ cd temp
$ ls
VMware-Workstation-Full-15.0.2-10952284.x86_64.bundle
```

## 更改文件权限

Linux系统对于文件的默认权限是`rw-rw-r--`，即文件主和文件主同组用户对该文件都是可读可写，而其他用户只能读，`bundle`文件是Linux下的可执行文件，类似于Windows中的`exe`文件，因此我们需要为其增加可执行权限。

```shell
$ ls -l
total 484052
-rw-rw-r-- 1 leslie leslie 495664015 2月   2 14:20 VMware-Workstation-Full-15.0.2-10952284.x86_64.bundle
$ chmod +x VMware-Workstation-Full-15.0.2-10952284.x86_64.bundle
$ ls -l
total 484052
-rwxrwxr-x 1 leslie leslie 495664015 2月   2 14:20 VMware-Workstation-Full-15.0.2-10952284.x86_64.bundle
```

## 安装VMware

执行`bundle`文件，VMware需要root权限，所以在前面添加上`sudo`。

```shell
$ sudo ./VMware-Workstation-Full-15.0.2-10952284.x86_64.bundle
Extracting VMware Installer...done.
```

然后选择接受协议，一路`next`下去就好了。

## 安装VMware Tools

> **VMware Tools**是**VMware**虚拟机中自带的一种增强工具，相当于VirtualBox中的增强功能（Sun VirtualBox Guest Additions），是**VMware**提供的增强虚拟显卡和硬盘性能、以及同步虚拟机与主机时钟的驱动程序。

简单地说，VMware Tools为你提供了诸如分辨率自适应（Autosize，虚拟机桌面大小与程序窗口保持一致）、主机与虚拟机之间剪贴板的共享（Clipboard Shared between Guest and Host）等功能，VMware默认是不安装的，需要手动进行配置。

VMware提供了多种方式进行安装：

## 使用VMware自带的VMware Tools安装包进行安装

> 官方教程：https://kb.vmware.com/articleview?docid=1022525&lang=zh_CN

1. 启动此虚拟机。

2. 使用具有管理员权限或root用户权限的帐户登录此虚拟机。

3. 选择（顶端选项卡）：VM > 安装VMware Tools。

4. 打开Ubuntu桌面上挂载的VMware Tools CD。

5. 右键单击类似于VMwareTools.x.x.x-xxxx.tar.gz的文件名，单击**复制**，然后选择**Ubuntu 桌面**保存文件。

6. 右键单击**Ubuntu 桌面**上的类似于VMwareTools.x.x.x-xxxx.tar.gz的文件名，单击解压到当前文件夹。

7. 打开一个终端窗口。在“终端”中，运行下面的命令以导航到vmware-tools-distrib文件夹：

   ```shell
   $ cd Desktop/vmware-tools-distrib
   ```

8. 运行下面的命令来安装VMware Tools：

   ```shell
   $ sudo ./vmware-install.pl -d
   ```

   **注意**：-d假定您希望接受默认设置。如果不使用-d，请按**Return**接受默认值或提供您自己的答案。

   *请在确保你对设置项有所了解的情况下去除参数`-d`*

9. 输入您的Ubuntu密码。

10. 在VMware Tools安装完毕后重新启动Ubuntu虚拟机。

## 使用open-vm-tools

1. 打开终端输入

   ```shell
   $ sudo apt-get update
   $ sudo apt-get install open-vm-tools -y 
   ```

2. 在`open-vm-tools`安装完毕后重新启动Ubuntu虚拟机。

{% note default %} 

经测试，[第二种方法](#使用open-vm-tools)安装的`open-vm-tools`只是[第一种方法](#使用VMware自带的VMware-Tools安装包进行安装)安装的完整版VMware Tools的一个子集，缺失了部分功能，其中一个重要的功能就是**剪贴板共享**，所以如果对该功能有强烈需求的用户，请使用第一种方法进行安装。

{% endnote %}

# 卸载

```shell
$ vmware-installer -u vmware-workstation
```

随后会跳出卸载界面，跟着提示卸载就行。

