---
title: "【教程】Manjaro安装Miniconda"
date: 2019-07-10 02:27:41
tags: [ "Manjaro", "Linux", "Conda", "Software" ]
categories: [ "教程" ]
keywords: ["manjaro", "conda"]
---

Manjaro Linux是基于Arch Linux的Linux发行版，在经过这段时间的使用之后原本信仰Ubuntu的我不禁说一句真香。

Conda是一个python的包管理/环境管理器，因为代码的新旧程度不同，有时候需要安装多个版本的python，Linux下还好些，Windows下对于这个问题的解决方案比较复杂，经常需要对本身的环境变量进行很多设置，在这种情况下Conda体现了它别样的魅力。话扯远了，这次正好记录一下在Manjaro安装Conda时碰到的问题及解决方法。

<!--more-->

## 安装

### pacman/yay安装

只需要一行代码就可以安装上：

```bash
# 使用pacman
$ sudo pacman -Ss miniconda3

# 使用yay
$ sudo yay -Ss miniconda3
```

### 手动安装

从清华TUNA镜像站的[Anaconda镜像](https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/)下载你所需要的版本，一般是将滚动条拉到最下面下载最新的版本也即`Miniconda-latest-**-**`，根据你的系统选择合适的版本。我选择的是`Miniconda3-latest-Linux-x86_64.sh`。

```bash
$ sh Miniconda3-latest-Linux-x86_64.sh
```

然后根据提示阅读并同意相关协议，选择安装位置开始安装，可以直接选择选默认的，一般是`$HOME/miniconda3`，可以修改但是需要记住修改后的位置，因为之后要用。

## 载入

在安装之后并不能直接用conda，还需要设置一下环境，将`miniconda3/bin`所在的位置加入`$PATH`变量中。

如果你使用的是默认的安装位置，使用你喜欢的编辑器，在你shell配置文件最后加入：

```bash
CONDA_PATH=$HOME/miniconda3
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('$CONDA_PATH/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "$CONDA_PATH/etc/profile.d/conda.sh" ]; then
        . "$CONDA_PATH/etc/profile.d/conda.sh"
    else
        export PATH="$CONDA_PATH/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

如果你修改了安装位置，那么修改第一行`$CONDA_PATH`的值为你的安装位置即可。

如果是使用pacman/yay安装的，安装路径可能是在`/opt/anaconda/bin`，检查一下路径的正确性然后修改`$CONDA_PATH`的值即可。

## Ubuntu安装Conda

只需要：

**Linux 64-bits**
```bash
bash <(curl -s -S -L "https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh")
```

**Linux 32-bits**
```bash
bash <(curl -s -S -L "https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86.sh")
```