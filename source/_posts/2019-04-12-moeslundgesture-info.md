---
title: "【笔记】数据集之12-MoeslundGesture"
date: 2019-04-17 10:58:30
tags: ["dataset", "deep-learning", "machine-learning"]
categories: ["Note"]
keywords: ["MoeslundGesture", "数据集"]

---

![](https://leslie-cloud.oss-cn-beijing.aliyuncs.com/2019/04/20190417-01-00.png)

最近在做散射场数据用来直接分类的一个项目，需要一些简单的、和人体姿态或手势姿态有关的数据集，先看了`FGnet`的数据集，发现不太符合我的要求，然后找到了这篇抽取自[Thomas Moeslund's Gesture Recognition](http://www-prima.inrialpes.fr/FGnet/data/12-MoeslundGesture/database.html)的一个叫做`12-MoeslundGesture`的手势数据集，下面简单介绍该数据集的具体参数。

翻译自：<http://www-prima.inrialpes.fr/FGnet/data/12-MoeslundGesture/database.html>

<!--more-->



---

该数据集由使用国际手语字母表中的不同静态符号的手的2100张图像组成。这个数据集最早出现在一篇于1996年发布的名为[Recognizing Gestures From the Hand Alphabet Using Principal Component Analysis](http://www-prima.inrialpes.fr/FGnet/data/12-MoeslundGesture/report.ps.Z)的硕士论文中，后来在[Real-Time Recognition of Hand Alphabet Gestures Using Principal Component Analysis](http://www.vision.auc.dk/~tbm/Publications/paper.ps.Z)这篇文章中也出现了它的精简版本。对该数据集有任何意见或问题都可以发送邮件至*tbm@cvmt.dk*。

数据集中的图像是分辨率为`248x256`，格式为`TIF`的灰度图片，每个手势都在深色背景前执行，并且用户的手臂覆盖有类似的黑色布料，使得分割背景变得更加容易，一共12个手势，不断地平移、旋转，从而拍摄得到了同一个手势的不同图片。

数据集具体参数如下：

| label | count | label | count | label | count | label | count |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| A     | 40    | H     | 100   | P     | 100   | W     | 100   |
| B     | 60    | I     | 100   | Q     | 100   | X     | 100   |
| C     | 40    | K     | 100   | R     | 100   | Y     | 100   |
| D     | 40    | L     | 100   | S     | 100   | AE    | 40    |
| E     | 40    | M     | 100   | T     | 100   |       |       |
| F     | 40    | N     | 100   | U     | 100   |       |       |
| G     | 100   | O     | 100   | V     | 100   |       |       |

可以在[这里](http://www-prima.inrialpes.fr/FGnet/data/12-MoeslundGesture/Gesture_images/database.tar)下载整个数据集，~~勤劳机智勇敢的~~我已经把它搬运到[百度云](https://pan.baidu.com/s/1ygAwEaaFYd6XmBmWdGr1-A)（提取码`m369`）了。

