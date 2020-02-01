---
title: "【LaTeX快速指南】（一）安装与配置中文环境"
date: 2019-11-20 22:54:40
mathjax: true
categories: ["Tutorial"]
tags: 
    - "LaTeX"
    - "tool"
---

![](https://leslie-cloud.oss-cn-beijing.aliyuncs.com/2019/11/2019-11-20-latex-tutorial-01-01.png)

{% cq %}
LaTeX（/ˈlɑːtɛx/，常被读作/ˈlɑːtɛk/或/ˈleɪtɛk/，写作$\LaTeX$），是一种基于TeX的排版系统，由美国计算机科学家莱斯利·兰伯特在20世纪80年代初期开发，利用这种格式系统的处理，即使用户没有排版和程序设计的知识也可以充分发挥由TeX所提供的强大功能，不必一一亲自去设计或校对，能在几天，甚至几小时内生成很多具有书籍质量的印刷品。对于生成复杂表格和数学公式，这一点表现得尤为突出。因此它非常适用于生成高印刷质量的科技和数学、物理文档。这个系统同样适用于生成从简单的信件到完整书籍的所有其他种类的文档。

——维基百科*https://zh.wikipedia.org/wiki/LaTeX*
{% endcq %}
<!--more-->

相比于常见的Word和WPS等所见即所得的文字处理软件，LaTeX更像是一个极客手中的玩具，许多人想要上手却因为它的学习曲线陡峭望而却步，事实上“会用”却并不难。这篇入门教程的初衷便是提供一个简洁明了的上手教程，降低入门难度。如果有使用Markdown的经验，那么LaTeX会让你有一种熟悉感。

**本人能力有限，水平一般，错漏难免，欢迎指正。**

## 安装LaTeX环境

安装LaTeX需要两步：

1. 安装TeX发行版：

    | Platform |     TeX Distribution                                             |
    | -------- |    ------------------------------------------------------------ |
    | Windows  |    [TeX Live](https://www.tug.org/texlive/), [CTeX](http://www.ctex.org/HomePage), [MiKTeX](https://mixtex.org) |
    | Linux    |    [TeX Live](https://www.tug.org/texlive/)                     |
    | macOS    |     [MacTeX](https://tug.org/mactex/), [TeX Live](https://www.tug.org/texlive/) |

   其中TeX Live是唯一支持全平台的发行版，Linux和Windows下都建议使用TeX Live，一键式安装，方便快捷，功能完善，少有bug。官网下载速度较慢，下附TeX Live的镜像下载地址。

   > 感谢TUNA协会对开源社区的支持！
   >
   > TeX Live 2019 下载地址：
   > 
   > https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/texlive2019-20190410.iso

   下载后解压，双击`install-tl-windows.bat`后在GUI里点击安装即可。

2. 安装TeX编辑器：
   TeX发行版和TeX编辑器的关系可以类比浏览器和Sublime/VSCode等编辑器的关系，浏览器负责对网页文件进行解析和渲染，VSCode则是用来编辑网页文件。后者不是必需的（甚至可以只用notepad），但一个好的编辑器可以极大地提升编辑体验和简化排版过程，推荐使用TeXStudio，另TeXLive自带了TeXworks，也可以直接使用。
   
   > TeXStudio下载地址：
   >
   > <http://texstudio.sourceforge.net/#download>

   选择与操作系统对应版本的安装包即可。

## LaTeX中文支持

LaTeX开发之初并未考虑到中文排版的需求，原生不支持中文输入，为此一群大佬开发了CTeX，虽然在三年前便停止了更新，但对于初学者而言，它仍是开箱即用的不二选择。

如果有自定义字体的需求，则可以使用xeCJK。

打开TeXStudio后使用`Ctrl+N`新建一个tex文件，键入：

{% tabs tex_code %}
<!-- tab ctex -->
```tex
% 文章类型
\documentclass{article}
% 导入包
\usepackage{ctex}
% --------------------------------------- %

% 文章信息
\title{ctex+xelatex中文支持}
\author{十一}
\date{\today}

% 文章内容
\begin{document}
\maketitle

% 摘要
\begin{abstract}
	这是一个测试用的摘要. \\
	This is a abstract for test.
\end{abstract}

\section{节1}
这是一个测试用的节
\subsection{节1.1}
这是一个测试用的小节
\subsection{节1.2}
这是一个测试用的小节

\end{document}
```
<!-- endtab -->

<!-- tab xelatex -->
```tex
% 文章类型
% 文章类型
\documentclass{article}
% 导入包
\usepackage{fontspec, xunicode, xltxtra}
\usepackage[slantfont,boldfont]{xeCJK}
\usepackage{lmodern}

% 字体映射
\defaultfontfeatures{Mapping=tex-text}

% 中文缩进
\XeTeXlinebreaklocale "zh"
\XeTeXlinebreakskip = 0pt plus 1pt minus 0.1pt

% 中文字体设置
% 这里字体可以自行替换，对应的分别是全局字体、无衬线字体和等宽字体
% 但要确保是系统中已有的字体
\setCJKmainfont{宋体}
\setCJKsansfont{微软雅黑}
\setCJKmonofont{仿宋}
%\setCJKmainfont{Adobe Song Std}
%\setCJKsansfont{Adobe Heiti Std}
%\setCJKmonofont{Adobe Fangsong Std}

% 文章信息
\title{ctex+xelatex中文支持}
\author{十一}
\date{\today}

% 文章内容
\begin{document}
\maketitle

% 摘要
\begin{abstract}
	这是一个测试用的摘要. \\
	This is a abstract for test.
\end{abstract}

\section{节1}
这是一个测试用的节
\subsection{节1.1}
这是一个测试用的小节
\subsection{节1.2}
这是一个测试用的小节

\end{document}
```
<!-- endtab -->

{% endtabs %}

差别只在于开始的几行代码，具体实现上可以任意套用其中的一种，然后点击菜单栏上的双绿色箭头（或F5）进行编译并显示即可，显示效果如下图所示：

![](https://leslie-cloud.oss-cn-beijing.aliyuncs.com/2019/11/2019-11-20-latex-tutorial-01-02.png)

## Q & A

{% note danger %}

**Fatal Package fontspec Error**

Question：代码提示`Fatal Package fontspec Error: The fontspec package requires either XeTeX or(fontspec) LuaTeX. \msg_fatal:nn {fontspec} {cannot-use-pdftex}`，如下：

![](https://leslie-cloud.oss-cn-beijing.aliyuncs.com/2019/11/2019-11-20-latex-tutorial-01-03.png)

Answer：**`fontspec`或`ctex`均只能使用xelatex作为编译命令，需要替换编译引擎为`XeLaTeX`，TeXStudio在`Option > Configure TeXStudio... > Build > Default Compiler`处设置，TeXworks在菜单栏处可以直接选择。**

{% endnote %}