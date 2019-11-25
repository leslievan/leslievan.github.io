---
title: "【教程】LaTeX中不能显示Adobe中文字体"
date: 2019-11-20 13:29:55
draft: false
categories: ["Tutorial"]
tags: ["latex", "linux", "manjaro", "ubuntu", "tool"]
---

![](https://leslie-cloud.oss-cn-beijing.aliyuncs.com/2019/11/2019-11-20-latex-cannot-display-adobe-font-01.png)

快毕业了，准备用LaTeX写论文，但LaTeX对于中文的支持并不是很好，在配置的过程中碰到了不少问题。
发行版是TeX Live 2019，参考复旦大学论文模板[fduthesis](https://ctan.math.illinois.edu/macros/latex/contrib/fduthesis/fduthesis.pdf)下载了Adobe的四种字体`宋体`、`黑体`、`仿宋`和`楷体`，足以用来应对绝大多数的中文论文。
但在设置好默认字体并成功编译后，却发现显示的是一片空白，尝试使用纯英文，同样无法显示。

<!--more-->

LaTeX是一种基于TeX的排版系统，常用于撰写学术论文，可以把它看做命令行/代码块版的Word，需要一定的学习成本，但熟练之后效率远超Word。

|  Item    |   Value  |
|----------|----------|
|操作系统   |**Manjaro Linux**|
|TeX发行版|**TeX Live 2019**|
|TeX编辑器|**TeXStudio**|

因为我的主力系统是Manjaro Linux，没法获得CTEX的加持，否则倒是能省下不少功夫。**如果你的系统是Windows，且不愿意过多折腾，建议直接使用[CTEX](http://www.ctex.org/CTeX)。**

## 故障分析

Linux下使用TeX Live编译输出PDF时，编译器不报错，但Adobe Font无法正常显示。

```latex
%!TEX program = xelatex
\documentclass[12pt,a4paper]{article}
\usepackage{fontspec,xunicode, xltxtra}
\usepackage{xeCJK}
\defaultfontfeatures{Mapping=tex-text}
\setCJKmainfont{Adobe Song Std}
\setmainfont{Source Han Serif}

\begin{document}
	This is a test document, we use Source Han Serif font for English. \\
	这是一个测试字体的文档，中文使用Adobe宋体。
\end{document}
```

如下图所示：

![](https://leslie-cloud.oss-cn-beijing.aliyuncs.com/2019/11/2019-11-20-latex-cannot-display-adobe-font-02.jpg)

## 解决方法

检查之后发现是内置的PDF渲染程序不支持Adobe Fonts，补齐相关依赖即可。

```shell
# Ubuntu
sudo apt-get install poppler-data

# Manjaro
sudo pacman -S poppler-data

# 其他发行版请自行修改安装命令
```

解决后显示结果如下图所示：

![](https://leslie-cloud.oss-cn-beijing.aliyuncs.com/2019/11/2019-11-20-latex-cannot-display-adobe-font-03.png)

## 引用

1. [latex 生成的 pdf 中 Adobe中文字体不能显示 - Ubuntu中文论坛](https://forum.ubuntu.org.cn/viewtopic.php?t=274815)
2. [Poppler - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/Poppler)