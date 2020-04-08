---
title: "【教程】Manjaro升级内核后无法打开VMware"
date: 2019-06-25 16:26:40
tags: [ "Linux", "Manjaro", "VMware", "Software" ]
categories: [ "Tutorial" ]
---
![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2019/06/20190625-00-00.jpg)
在Ubuntu又一次搞坏了CUDA的驱动之后，我投向了Manjaro的怀抱，重新进入了双系统的状态，VMware还是要安装的，安装的步骤倒是和Ubuntu没有什么不同。Manjaro默认的内核头文件是3.16版本的，我升级到了和内核相匹配的4.19，然后就出问题了，找了几种方法后终于解决，遂记录于此，万一下次还碰到了呢？

<!--more-->

## 故障分析

- 更新了内核 || 启用安全启动了UEFI引导
- 发现错误：
  `Cannot open /dev/vmmon: No such file or directory. Please make sure that the kernel module 'vmmon' is loaded`

## 解决方法

### VMware Forum[Unsolved]

1. Generate a key pair using the openssl to sign vmmon and vmnet modules:
   ```bash
   $ openssl req -new -x509 -newkey rsa:2048 -keyout MOK.priv -outform DER -out MOK.der -nodes -days 36500 -subj "/CN=VMware/"
   ```
   
2. Sign the modules using the generated key by running these commands:

   ```bash
   $ sudo /usr/src/linux-headers-`uname -r`/scripts/sign-file sha256 ./MOK.priv ./MOK.der $(modinfo -n vmmon)
   $ sudo /usr/src/linux-headers-`uname -r`/scripts/sign-file sha256 ./MOK.priv ./MOK.der $(modinfo -n vmnet)
   ```

3. Import the public key to the system's MOK list by running this command:

4. Confirm a password for this MOK enrollment request.

5. Reboot your machine. Follow the instructions to complete the enrollment from the UEFI console.

### Manjaro Forum[Solved]

```bash
$ git clone https://github.com/mkubecek/vmware-host-modules
$ cd vmware-host-modules && git checkout -t origin/workstation-xx.x.x
$ make
$ sudo make install && modprobe --force-vermagic -a vmw_vmci vmmon
```

将第二行中的`xx.x.x`换成vmware对应的版本号即可

## 讨论

很遗憾VMware官方所描述的方法没（然）有（并）用（卵），因为Manjaro我根本找不到它的`linux-headers`在哪里……令人窒息，Manjaro论坛里面给出的解决方案和VMware官方的本质上是一样的，都是让`vmmon`通过内核的模块验证，这里就牵扯到了Linux内核模块的版本检查机制，内核在装载模块的时候会使用CRC和Vermagic两种解决方法，后者保存了模块编译时的内核版本以及SMP等配置信息，似乎是编译`vmmon`时所用的内核和当前内核版本不一致导致了这个问题。

PS：官方给的方案更复杂一点……总给我一种比后者更安全的感觉，不过我还是选择简单的:grin:（误）。

## 引用

1. ["Cannot open /dev/vmmon: No such file or directory" error when powering on a VM (2146460)](https://kb.vmware.com/s/article/2146460)
2. [Vmware vmmon module error](https://forum.manjaro.org/t/vmware-vmmon-module-error/39429)
3. [VMware (简体中文) - ArchWiki](https://wiki.archlinux.org/index.php/VMware_(简体中文))
4. [SDB_安装 VMware - openSUSE Wiki](https://zh.opensuse.org/SDB:%E5%AE%89%E8%A3%85_VMware)