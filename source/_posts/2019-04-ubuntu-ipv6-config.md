---
title: "【教程】Ubuntu使用IPv6拨号连接"
date: 2019-04-24 22:18:29
tags: ["Ubuntu", "DNS", "Network"]
categories: ["Tutorial"]
---

> **IPv6**是下一版本的互联网协议，也可以说是下一代互联网的协议，它的提出最初是因为随着互联网的迅速发展，**IPv4**定义的有限地址空间将被耗尽，地址空间的不足必将妨碍互联网的进一步发展。 为了扩大地址空间，拟通过**IPv6**重新定义地址空间。**IPv6**采用128位地址长度，几乎可以不受限制地提供地址。

<!--more-->



## Use IPv6

拨号连接默认不使用`IPv6`，但提供了简单的操作让我们去设置`IPv6`，使用`man pppd | grep ipv6`可以看到：

```shell
$ man pppd | grep ipv6
       +ipv6  Enable the IPv6CP and IPv6 protocols.
       ipv6 <local_interface_identifier>,<remote_interface_identifier>
              ipv6cp-use-ipaddr option is given, the local identifier  is  the
              MAC address, ipv6cp-use-persistent option can be used to replace
              the ipv6 <local>,<remote> option. Otherwise  the  identifier  is
       ipv6cp-accept-local
       ipv6cp-accept-remote
       ipv6cp-max-configure n
       ipv6cp-max-failure n
       ipv6cp-max-terminate n
       ipv6cp-restart n
       noipv6 Disable  IPv6CP  negotiation and IPv6 communication. This option
       /etc/ppp/ipv6-up
       /etc/ppp/ipv6-down
              with the same parameters as the ipv6-up script.
```

第一行就提供了一个参数，用以支持`IPv6`，我们只需要在配置文件`/etc/ppp/peers/dsl-provider`中添加一行`+ipv6`即可：

```shell
$ sudo echo "+ipv6" >> /etc/ppp/peers/dsl-provider
```

## Set DNS

Ubuntu 18.04使用`systemd-resolved`管理DNS。

>有三种处理 /etc/resolv.conf 文件(参见 resolv.conf(5)) 的方式：
>
>- 创建 /etc/resolv.conf 软连接，并将其指向 /usr/lib/systemd/resolv.conf 文件(其中仅设置了单独一个 127.0.0.53 DNS服务器)。 这是推荐的首选方式。
>- 创建 /etc/resolv.conf 软连接， 并将其指向由 systemd-resolved 实时更新的 /run/systemd/resolve/resolv.conf 文件。 注意，此文件中只包含所有已知的全局DNS服务器，而不包含针对特定网络接口设置的DNS服务器。 注意，应用程序不应该直接使用 /run/systemd/resolve/resolv.conf 文件， 而是应该继续使用 /etc/resolv.conf 文件。 使用这种方式，所有绕过本地 DNS API 的客户端也将同样绕开 systemd-resolved 服务， 直接使用已知的DNS服务器。
>- 由其他软件包或系统管理员维护 /etc/resolv.conf 的内容。 在这种情况下， systemd-resolved 将会从中读取全局DNS配置。 也就是说，systemd-resolved 只是一个读取 /etc/resolv.conf 配置文件的使用者， 而非此文件的提供者。

注意，上述三种处理方式是自动感知的(不需要特别的配置)，完全取决于 /etc/resolv.conf 是否为软连接， 以及软连接指向的目标。

在这里我们使用最后一种方法，在`Home`目录下创建一个配置文件，填入我们想要使用的DNS地址，然后将其软链接到`/etc/resolv.conf`。

```shell
$ cd ~
$ touch .resolv.conf
$ echo "nameserver 240c::6666\nnameserver 240c::6644" >> ~/.resolv.conf
$ sudo rm /etc/resolv.conf && sudo ln -s ~/.resolv.conf /etc/resolv.conf
```

执行完以上命令你可以使用`systemd-resolve --status`，使用键盘上的:arrow_down:滚动输出，找到拨号连接（一般是`ppp*`），即可查看当前的DNS设置是否生效。

## Reference

1. [IPv6 DNS 免费公共服务器地址大全Public IPv6 DNS Server - DNS ...](https://dns.icoa.cn/ipv6/)
2. [systemd-resolved.service 中文手册 [金步国]](<http://www.jinbuguo.com/systemd/systemd-resolved.service.html>)
3. [IPv6 Over PPPoE - Google 网上论坛](<https://groups.google.com/forum/#!topic/xidian_linux/p3XW0jJz4Wo>)

