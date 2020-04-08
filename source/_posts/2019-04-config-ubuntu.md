---
title: "【笔记】Ubuntu美化装机全步骤"
date: 2019-04-17 00:32:48
tags: [ "Ubuntu", "Software", "Gnome"]
categories: [ "笔记" ]
keywords: [ "Ubuntu", "装机", "美化" ]
---

Ubuntu重装了太多太多次，这次因为安装CUDA，结果把显卡驱动弄坏了，折腾了半小时没救回来，遂重装了事，记录下一系列的步骤，步骤仅供我自己参考，~~如有按图索骥然后弄崩系统的，概不负责~~，有兴趣参考的可以邮件给我或在下方评论。

<!--more-->



## Theme

### Font & Icon & Cursor

```shell
# fonts
$ mkdir .fonts
$ cp themes/fonts/* .fonts
$ mkfontscale && mkfontdir && fc-cache -fv

# icon
$ sudo dpkg -i install themes/papirus-icon-theme_*.deb

# cursor
$ mkdir .icons
$ cp themes/icons/* .icons

# shell color theme
$ cd themes
$ ./gosh.sh
```

### Theme

```shell
$ sudo apt-get install gnome-tweak-tool gnome-shell-extensions
$ sudo /etc/init.d/gdm3 restart

$ git clone https://github.com/vinceliuice/vimix-gtk-themes.git vimix
$ cd vimix
$ ./vimix-installer
```

### Time Language

```shell
$ vim /etc/default/locale
:%s/zh_CN/en_US/g
:x
```



## Driver

### Display

```shell
$ sudo apt-get install nvidia-361
$ reboot
```

### Printer

```shell
$ hp-setup -i
```



## Software

### Fcitx & SogouPinyin

```shell
$ sudo apt-get install fcitx
$ sudo dpkg -i sogoupinyin_2.2.0.0108_amd64.deb
Selecting previously unselected package sogoupinyin.
(Reading database ... 150921 files and directories currently installed.)
Preparing to unpack .../sogoupinyin_2.2.0.0108_amd64.deb ...
Unpacking sogoupinyin (2.2.0.0108) ...
dpkg: dependency problems prevent configuration of sogoupinyin:
 sogoupinyin depends on libfcitx-qt0 | fcitx-libs-qt; however:
  Package libfcitx-qt0 is not installed.
  Package fcitx-libs-qt is not installed.
 sogoupinyin depends on libopencc2 | libopencc1; however:
  Package libopencc2 is not installed.
  Package libopencc1 is not installed.
 sogoupinyin depends on fcitx-libs (>= 4.2.7); however:
  Package fcitx-libs is not installed.
 sogoupinyin depends on libqtwebkit4 (>= 2.1.0~2011week13); however:
  Package libqtwebkit4 is not installed.

dpkg: error processing package sogoupinyin (--install):
 dependency problems - leaving unconfigured
Processing triggers for mime-support (3.60ubuntu1) ...
Processing triggers for libglib2.0-0:amd64 (2.56.3-0ubuntu0.18.04.1) ...
No such key 'Gtk/IMModule' in schema 'org.gnome.settings-daemon.plugins.xsettings' as specified in override file '/usr/share/glib-2.0/schemas/50_sogoupinyin.gschema.override'; ignoring override for this key.
Processing triggers for gnome-menus (3.13.3-11ubuntu1.1) ...
Processing triggers for desktop-file-utils (0.23-1ubuntu3.18.04.2) ...
Processing triggers for shared-mime-info (1.9-2) ...
Processing triggers for hicolor-icon-theme (0.17-2) ...
Errors were encountered while processing:
 sogoupinyin

$ sudo apt-get -f install
$ reboot
```

### VMware



### Typora

```shell
# or run:
# sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BA300B7755AFCFAE
wget -qO - https://typora.io/linux/public-key.asc | sudo apt-key add -

# add Typora's repository
sudo add-apt-repository 'deb https://typora.io/linux ./'
sudo apt-get update

# install typora
sudo apt-get install typora
```

### Network

**Shadowsocks && Privoxy**

```shell
# Install
$ sudo apt-get install privoxy shadowsocks

# Config
$ sudo vim /etc/shadowsocks/config.json
$ sudo vim /etc/privoxy/config

# Start
$ sslocal -c /etc/shadowsocks/config
$ service privoxy start
```

### Hugo

```shell
$ git clone https://github.com/gohugoio/hugo.git $GOPATH/hugo
$ cd $GOPATH/hugo
$ go install
$ export 
```

### Some...

```shell
$ sudo dpkg -i opt/deb/*
$ sudo apt-get -f install
```



## Configuration

### pip mirror

```shell
$ mkdir .pip
$ touch .pip/pip.conf
$ echo '[global]\nindex-url = https://pypi.tuna.tsinghua.edu.cn/simple\n[install]\ntrusted-host = pypi.tuna.tsinghua.edu.cn' > .pip/pip.conf
```

### apt mirror

```shell
python3 config/oh-my-tuna.py
```

### Some...

```shell
$ sudo apt-get install zsh zsh-antigen git curl vim silversearcher-ag redshift trash-cli aria2
```

| opt               | function                                                     |
| ----------------- | ------------------------------------------------------------ |
| zsh               | A shell designed for interactive use                         |
| zsh-antigen       | A small set of functions that help you easily manage your shell(zsh) plugins |
| git               | A free and open source distributed version control system    |
| curl              | A command line tool and library for transferring data with URL syntax |
| vim               | A greatly improved version of the good old UNIX editor Vi    |
| silversearcher-ag | A code searching tool similar to `ack`, with a focus on speed. |
| redshift          | Adjusts the color temperature of your screen according to your surroundings. |
| trash-cli         | Command Line Interface to FreeDesktop.org Trash.             |
| aria2             | Aria2 is a lightweight multi-protocol & multi-source command-line download utility. |

---
#### shell

修改默认shell

```shell
$ chsh -s /bin/zsh
```

#### aria2

```shell
# Edit config
$ vim ~/.config/.aria2.conf

# Start aria2c
$ aria2c --conf-path ~/.config/.aria2.conf
```

#### git

```shell
$ git config --global user.name 'username'
$ git config --global user.email 'useremail'
```

#### apt-fast

```shell
$ sudo add-apt--repository ppa:apt-fast/stable
$ sudo apt-get update
$ sudo apt-get install apt-fast
$ reboot
```

## Coding

### Jetbrains

Install Jetbrains ToolBox.

### Python

```shell
$ sudo apt-get install python3-pip python3-opencv
$ pip3 install numpy torch scipy PIL
```

### CUDA

```shell
# Disable graphical target first.
$ sudo systemctl set-default multi-user.target
$ reboot

# Login, and install without driver first. Be silent to install driver next.
$ sudo sh cuda_10.1.105_418.39_linux.run --silent --driver

# Enable graphical target.
$ sudo systemctl set-default graphical.target
$ reboot
```

### Go

```shell
$ tar -C /usr/local -xzf go1.12.4.linux-amd64.tar.gz
$ export PATH=$PATH:/usr/local/go/bin
```
