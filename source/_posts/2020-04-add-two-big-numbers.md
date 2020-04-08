---
title: 【算法】大数加法
date: 2020-04-03 16:22:44
tags: ["大数问题", "算法"]
categories: ["问题", "算法"]
mathjax: true
---

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2020/04/2020-04-add-two-big-numbers-00.png)

大数加法即能够对超长位数的数字进行相加，比如一个100位数和一个80位数的数字相加。

在这种情况下，数的大小已经超出了基本类型（int,long,double,float）能够表示的范围，直接加减只能得到错误的结果，想要得到正确的结果就需要使用其他数据结构存储这些数字，同时构建相应的相加函数，这里应该想到可以使用占用空间可选的字符串类型。

<!--more-->

## 问题抽象

输入为(M,N):

- M: 字符串`string`存储的10进制整数$M$
- N: 字符串`string`存储的10进制整数$N$

输出为S:

- S: 字符串`string`存储的10进制大数$S$

## 数学原理

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2020/04/2020-04-add-two-big-numbers-01.gif)

写出计算一般数加法的步骤，如上图。可以看到，每一次循环涉及到两个加数当前位`a`,`b`、进位`carry`和结果位`result`，关系如下：

```text
carry = (a + b) // 10
result = (a + b) % 10
```

循环至两个数结束，若其中一个数长度小于另外一个数，则该数当前位使用0进行计算。

## 代码实现

这里给出C++的算法实现，使用了大量内置的STL，如不能使用STL库可自行实现相关类型。

```c++
/**
 * Created by Leslie
 * 2020-03-28
 */

#include "string"
#include "algorithm"

using namespace std;

/**
 * Add two big decimal numbers
 * @param a string of a big number
 * @param b string of a big number
 * @return string of the result
 */
string AddTwoNumbers(string a, string b) {
    int x, y, sum, carry = 0;
    string result;
    auto iter_a = a.rbegin(), iter_b = b.rbegin();

    while (iter_a != a.rend() || iter_b != b.rend()) {
        // 其中一个数长度小于另外一个数，则遍历该数不存在的高位时，用0替代
        x = iter_a != a.rend() ? *iter_a - '0' : 0;
        y = iter_b != b.rend() ? *iter_b - '0' : 0;
        
        sum = x + y + carry;
        carry = sum / 10;
        result += char(sum % 10 + '0');
		
        // 遍历到最后一位时，迭代器不再移动
        if (iter_a != a.rend()) {
            iter_a++;
        }
        if (iter_b != b.rend()) {
            iter_b++;
        }
    }

    // 最高位存在进位
    if (carry == 1) {
        result += char(carry + '0');
    }

    reverse(result.begin(), result.end());
    return result;
}

```

这里的`string`类型完全可以使用`char*`替代，可以尝试使用C进行实现。

