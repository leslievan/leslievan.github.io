---
title: 【算法】2019年南京大学计算机考研复试机试题分享
date: 2020-03-02 14:52:56
tags: [ "Algorithm" ]
categories: [ "Note" ]
mathjax: true
keywords: ["nju", "postgraduate", "algorithm", "c++"]
---

2019年南京大学计算机考研复试机试题分享（个人算法+最优解法）

题目来源：[HDU-ACM](http://acm.hdu.edu.cn/diy/contest_show.php?cid=36342)

**Problems**
- [Stepping Numbers](/2020/03/nju-postgradute-retry/#stepping-numbers)
- Nodes from the Root
- Distinct Subsequences

<!--more-->

## Stepping Numbers

**问题简述**
Stepping Numbers（以下简称步进数）是符合以下定义的整数：
任意两个相邻数字的差之绝对值都为1，则该数字称为步进数。步进数至少包含2位数字。
如`321`是步进数，但`421`不是。
给定两个整数$M$ 和$N$，计算$[M,N]$范围内所有步进数的数量。（其中$M \le N,N \le 3e8$）

**输入样例**
```plain
1
2 21
```

**输出样例**
```plain
3
(hint:  Stepping numbers between 2 and 21 are 10, 12 and 21.)
```

**解题思路**
直接暴力遍历，复杂度太高,每次运算都需要$3e8$次判断。
可以看到的是，