---
title: 【算法】大数任意进制转换
date: 2020-03-29 15:48:47
tags: ["Alogorithm", "big-number"]
categories: ["Note"]
mathjax: true
---

![](https://leslie-cloud.oss-accelerate.aliyuncs.com/2020/03/2020-03-big-number-base-convert-00.jpg)

写算法题的时候经常会碰到一些大数相关的问题，比如大数乘法、大数加法等等，乘法和加法的原理基本上都比较符合正常的思维模式，因为加法和乘法的原理相对清晰，模拟数学计算步骤可以方便地分离，并转换为代码。

相对于常见的加法和乘法，进制转换出现的频率低一些，但同样是一个十分值得探讨的问题，并且难度较之加法和乘法更高。

<!--more-->


## 问题抽象

输入为(M, m, n):

- M: m进制大数$M_m$，用字符串类型`string`储存
- m: 大数基数m
- n: 大数目的基数n

输出为N：

- N: n进制大数$N_n$，用字符串类型`string`储存

## 数学原理

m进制转换成n进制，通常采用的是「模n取余法」，一般数进制转换的方法：

```python
# num
result = []
temp = num
while temp > 0:
    reminder = temp % to_base
    quotient = temp // to_base
    result.append(reminder)
    temp = quotient
   
reveres(result)
    
```

> eg. $30\to(11110)_2$
>
> 30 / 2 = 15, 0
> 15 / 2 = 7, 1
> 7 / 2 = 3, 1
> 3 / 2 = 1, 1
> 1 / 2 = 0, 1

第一次的商被用作第二次的除数，**循环直至商为0**，先余为低位，后余为高位，转换后的数为余数组的逆序。

可以想象，大数转换步骤同样如此。

问题只在于大数的**整除**和**取余**，这里直接将算法解释如下：

```python
quotient = []
temp = 0
for i in big_num:		# 从大数中取位，取至最后一位循环停止
    temp *= src_base    # 余数乘以原基数
    temp += i           # 并加上当前位
    if temp < to_base:	# 如果该数小于目标基数，商位上0
        quotient.append('0')
        continue
    else				# 如果该数大于目标基数，上商，余数留给下一次运算
        quotient.append(temp / to_base)
        temp %= to_base
        
reminder = temp
quotient = remove_front_zero(quotient)

```

> eg. $(11110)_2\to 30$
>
> | 序号 | 当前位 | 运算                    | 商   | 余数 |
> | ---- | ------ | ----------------------- | ---- | ---- |
> | 0    | null   | null                    | null | 0    |
> | 1    | 1      | (0 * 2 + 1) / 10 = 0, 1 | 0    | 1    |
> | 2    | 1      | (1 * 2 + 1) / 10 = 0, 3 | 0    | 3    |
> | 3    | 1      | (3 * 2 + 1) / 10 = 0, 7 | 0    | 7    |
> | 4    | 1      | (7 * 2 + 1) / 10 = 1, 5 | 1    | 5    |
> | 5    | 0      | (5 * 2 + 0) / 10 = 1, 1 | 1    | 0    |
>
> 故$(11110)_2/10=(00011)_2,0=(11)_2$，余数为0
>
> 将$(11)_2$用作运算数
>
> | 序号 | 当前位 | 运算                    | 商   | 余数 |
> | ---- | ------ | ----------------------- | ---- | ---- |
> | 0    | null   | null                    | null | 0    |
> | 1    | 1      | (0 * 2 + 1) / 10 = 0, 0 | 0    | 1    |
> | 2    | 1      | (1 * 2 + 1) / 10 = 0, 3 | 0    | 3    |
>
> 故$(11)_2/10=(00)_2=0$，余数为3
>
> 得到余数组`03`，逆序后得到进制转换后的数`30`

## 代码实现

这里给出C++的算法实现，使用了大量内置的STL，如不能使用STL库可自行实现相关类型。

```cpp
#include "string"
#include "iostream"
#include "vector"
#include "algorithm"

using namespace std;

/**
 * Mapping a n-base number to a int number
 * @param c the n-base number
 * return the int number
 */
int GetValue(char c) {
    if (c >= '0' && c <= '9') {
        return c - '0';
    }
    if (c >= 'a' && c <= 'z') {
        return c - 'a' + 10;
    }
    if (c >= 'A' && c <= 'A') {
        return c - 'A' + 36;
    }
    return -1;
}

/**
 * Convert a big num between different base.
 * @param a the string of big num
 * @param src_base the base of origin number,
 * @param to_base
 * @return the sring of big num in src_base
 */
string BaseConvert(string a, int src_base, int to_base = 10) {
    if (src_base < 2 || src_base > 62 || to_base < 2 || to_base > 62) {
        return reinterpret_cast<const char *>(1);
    }

    char num_alpha[] = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
    int temp = 0;
    vector<int> number, quotient, result;
    string s;

    // 将字母映射为数字
    for (char &c : a) {
        number.push_back(GetValue(c));
    }
    auto iter = number.begin();

    while (!number.empty()) {
        // 得到余数和商
        while (iter != number.end()) {
            temp *= src_base;
            temp += *iter++;
            if (temp < to_base) {
                quotient.push_back(0);
                continue;
            } else {
                quotient.push_back(temp / to_base);
                temp %= to_base;
            }
        }
        // 得到余数，存入result
        result.push_back(temp);
        
        // 清空商的前置0
        auto i = quotient.begin();
        while (*i == 0 && i != quotient.end()) { i++; }
        if (i != quotient.begin()) {
            quotient.erase(quotient.begin(), i);
        }

        // 将商作为下一次的运算数，重置商数组和temp
        number = quotient;
        quotient.clear();
        iter = number.begin();
        temp = 0;
    }

    // 逆序余数位
    reverse(result.begin(), result.end());
    // 将数字映射为字母
    for (int &i:result) {
        s += num_alpha[i];
    }

    return s;
}

int main() {
    cout << BaseConvert("11110", 2, 10) << endl;
    cout << BaseConvert("30", 10, 2) << endl;

    return 0;
}
```

