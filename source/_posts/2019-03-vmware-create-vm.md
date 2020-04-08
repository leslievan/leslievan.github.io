---
title: "【教程】VMware Workstation中创建Ubuntu虚拟机"
tags: [ "Linux", "Ubuntu", "Software", "VMware" ]
categories: [ "教程" ]
date: 2019-03-05 14:40:08
keywords: ["vmware", "虚拟机"]

---

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-0.png)

简单描述如何使用VMware Workstation Pro创建一个新的虚拟机。

<!--more-->



# 准备工作

在开始创建新的虚拟机之前，你需要在本机上安装VMware Workstation，并准备好相应的镜像。

关于安装VMware Workstation，你可以参考[这篇文章](/2019/02/ubuntu-config-vmware/)。

至于镜像，你可以直接百度搜索官方网站进行下载，但不推荐这种方法，Linux发行版的网站服务器大多都在国外，因此下载速度会很慢，国内有许多镜像站可以用于下载镜像，如阿里的[OSPX](https://opsx.alibaba.com/)，清华的[清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn)等，这里提供两个网站的`Ubuntu 16.04 LTS`和`Ubuntu 18.04 LTS`的下载地址：

**OSPX**
- [Ubuntu 16.04](https://mirrors.aliyun.com/ubuntu-releases/xenial/ubuntu-16.04.6-desktop-amd64.iso)
- [Ubuntu 18.04](https://mirrors.aliyun.com/ubuntu-releases/releases/18.04.2/ubuntu-18.04.2-desktop-amd64.iso)

**清华大学开源软件镜像站**

- [Ubuntu 16.04](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/xenial/ubuntu-16.04.6-desktop-amd64.iso)
- [Ubuntu 18.04](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/bionic/ubuntu-18.04.2-desktop-amd64.iso)

到此，准备工作完成，你拥有了一台安装好`VMware Workstation`的电脑以及一个名为`ubuntu-xx.xx.x-desktop-amd64.iso`的镜像文件。

# 创建步骤

对于诸如Ubuntu、Windows等一些常见的操作系统，VMware Workstation提供了简易安装的方式，免去一些安装步骤，降低用户使用难度，适合新手玩家。

## 打开VMware

打开VMware，点击`Create a New Virtual Machine`（中文下应为创建新的虚拟机，之后不再提示）。

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-1.png)

## 选择安装方式

这里我们使用推荐的安装方式，选择`Typical`，点击`Next`。

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-2.png)

---

这里有两种安装方法，[简易安装](#简易安装)以及[手动安装](#手动安装)，简易安装方便快捷，但安装过程中可能会出现一些玄学问题，手动安装稍显麻烦，但好在依据步骤则不会出现问题，而且某种程度上可以学到更多的东西。

## 简易安装

你可以先创建虚拟机，之后再选择镜像（第三项），类似于你买了电脑，但是里面并没有预先安装任何系统，这里我们选择第二项`Use ISO Image`，在创建虚拟机之后直接安装系统，点击`Browse`选择你刚刚下载的镜像文件，然后点击`Next`。

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-3.png)

## 指定简易安装信息

填写空着的四项内容，点击`Next`。

| 简易安装提示 | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| Full name    | 所创建客户机的全名，可任意输入。                             |
| User name    | 用户名，用户标识符，表明你的身份，配合`Password`用于登陆Ubuntu。 |
| Password     | 密码，即你创建用户的密码。                                   |
| Confirm      | 验证密码，重新输入以上的密码。                               |

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-4.png)

## 指定虚拟机名称和文件位置

这里的`Name`和`Location`都可以任意选择，我直接使用默认的配置，点击`Next`。

| 简易安装提示 | 说明                                               |
| ------------ | -------------------------------------------------- |
| Name         | 虚拟机名称，可任意输入。                           |
| Location     | 虚拟机文件所在位置，尽量选择一个剩余容量大的磁盘。 |

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-5.png)

## 为虚拟机指定磁盘容量

注意容量是`Maximum disk size`而不是你一开始就分配这么多空间，所以你大可以分配一个大一点的空间，**千万别使用推荐配置中的20GB！**这里我直接给了100GB，基本上怎么折腾都足够了，如果你在这里直接选择了20GB，别急，也有补救措施，这篇文章会给你答案。

至于下面两个选项，一个是以单文件存储，一个是多文件存储，选择单文件存储意味着，最大容量100GB的内容都会存储在一个单独的文件中，而多文件存储则是每使用4GB空间就创建一个新的文件，即你用完100GB空间后，会生成25个文件，我并未比较过两种方式的优劣，但基本不影响我们使用系统，这里直接以默认的多文件存储方式安装。

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-6.png)

## 自定义虚拟机硬件

在这里可以修改默认的硬件设置，包括内存分配、虚拟 CPU 数量、CD/DVD 和软盘驱动器设置以及网络连接类型。

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-7.png)

点击`Customize Hardware…`进行自定义，可能需要修改的地方有两个。

- 内存（Memory）。如果物理机内存在8G以下，建议你只需要按照默认配置分配2G给虚拟机，如果物理机内存在8G及8G以上，则可以分配4G及4G以上的空间，至少需要留出1/2的最大内存以满足物理机运行需要（不会卡顿）。
- 处理器（Processors）。处理器影响多线程工作效率，默认为单核心单处理器，这里可以修改为双核心双处理器（2×2）。

其他属性不建议新手玩家修改，修改完之后点击`Close`保存配置，返回主界面，然后点击`Finish`。

简易安装的步骤到这里就结束了，不过简易安装不一定适用于所有人，可能会出现一些小问题，如果有问题可以在最后留言。

## 手动安装

手动安装稍显麻烦，前面两个步骤[打开VMware](#打开VMware)和[选择安装方式](#选择安装方式)都和简易安装一样，在选择镜像时才出现差异，这里略去前两步，直接从第三步开始选择第三项`I will install the operating system later`而不是第二项`Use ISO image`，然后点击`Next`。

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-8.png)

## 创建虚拟机

这一步根据你的镜像选择虚拟机类型，之前下载的镜像为`Ubuntu 16.04`或`Ubuntu 18.04`，均为64位的Linux发行版（Ubuntu同样提供32位，我们使用的是64位的），选择后点击`Next`。

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-9.png)

接下来的几个步骤同上面一样，[指定虚拟机名称和文件位置](#指定虚拟机名称和文件位置)->[为虚拟机指定磁盘容量](#为虚拟机指定磁盘容量)->[自定义虚拟机硬件](#自定义虚拟机硬件)，然后点击`Finish`，完成创建。

## 安装系统

虚拟机创建完成后，会跳转到如下图所示的界面：

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-10.png)

双击箭头所示的`CD…`，在弹窗中选择`Use ISO image`，选择你想要安装的镜像：

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-19.png)

点击`Save`后，启动虚拟机：

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-11.png)

### 选择语言

如果镜像没有问题的话，VMware会自动打开镜像，提示选择语言，准备进行安装：

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-12.png)

### 选择键盘布局

使用默认选项即可，直接`继续`。

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-13.png)

### 选择安装方式

最小安装省略了如LibreOffice之类的办公软件，基本上我们是不会用到的，最小安装可以极大地提升安装速度，推荐选择，当然玩家也可以自行斟酌，选择正常安装也是可以的。

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-14.png)

### 选择安装类型

直接选择第一项就可以了，这里的清除整个磁盘指的不是主机的磁盘，而是虚拟机的磁盘，所以不需要考虑，也可以自行尝试`其它选项`，点击`现在安装`：

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-15.png)

点击`继续`：

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-16.png)

### 选择地区

它会默认检测，如不需要特殊配置直接`继续`就行：

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-17.png)

### 指定Ubuntu安装信息

这里参考[指定简易安装信息](#指定简易安装信息)。

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-18.png)

### 重启系统

点击`继续`后，如无特殊事件只需静静等待，直到出现以下界面，选择`现在重启`：

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/03/2019-03-05-7e1ef425-20.png)

有时你可能需要根据提示，按下Enter自行重启。

## VMware Tools配置

参考另一篇文章：[Ubuntu下配置VMware Workstation](/2019/02/ubuntu-config-vmware/#安装vmware-tools)

---

至此，安装完成，你可以开心地使用你的虚拟机了！