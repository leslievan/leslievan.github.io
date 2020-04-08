---
title: 【机器学习】PyTorch构建自己的数据集
tags: ["机器学习", "PyTorch"]
categories: ["笔记"]
date: 2019-12-04 23:38:48
---



Python和MATLAB是机器学习最常用的两种开发工具，相比于MATLAB，Python的优势在于其免费使用以及开源，普通学生难以负担MATLAB的昂贵费用。机器学习的快速发展，推动了各种机器学习框架的出现，常见的机器学习框架如`TensorFlow`（Google）、`PyTorch/Torch`（Facebook）、`Caffe`（UC Berkeley）等。

PyTorch内置了诸如MNIST、cifar10等在内的一系列数据集，简单的几行代码就可以调用：

```python
import torch
from torchvision import datasets, transforms

train_loader = torch.utils.data.DataLoader(
    datasets.MNIST('../data', train=True, download=True,
                    transform=transforms.Compose([
                        transforms.ToTensor(),
                        transforms.Normalize((0.1307,), (0.3081,))
                    ])),
    batch_size=batch_size, shuffle=True)
test_loader = torch.utils.data.DataLoader(
    datasets.MNIST('../data', train=False, transform=transforms.Compose([
        transforms.ToTensor(),
        transforms.Normalize((0.1307,), (0.3081,))
    ])),
    batch_size=batch_size, shuffle=True)
```

那么如何自定义数据集呢？

<!--more-->

对PyTorch没有一点了解的可以先看这篇官方教程：[Introduction · Pytorch 中文文档](https://pytorch.apachecn.org/)

---

## 摘要

PyTorch内置抽象类`torch.utils.data.Dataset`，定义自己的数据集时，只需要继承该类，并重写其中的`__len__`和`__getitem__`。

```python
class Dataset(object):
    """An abstract class representing a Dataset.

    All other datasets should subclass it. All subclasses should override
    ``__len__``, that provides the size of the dataset, and ``__getitem__``,
    supporting integer indexing in range from 0 to len(self) exclusive.
    """

    def __getitem__(self, index):
        raise NotImplementedError

    def __len__(self):
        raise NotImplementedError

    def __add__(self, other):
        return ConcatDataset([self, other])

```

## 实现

**切分数据集**

首先准备好自己的数据集，将测试集和训练集分别置于`data/train`和`data/test`中，组织文件结构如下：
```text
.
├── data
│   ├── test
│   │   ├── 1.jpg
│   │   ├── 2.jpg
│   │   └── ...
│   ├── test.txt
│   ├── train
│   │   ├── 1.jpg
│   │   ├── 2.jpg
│   │   └── ...
│   └── train.txt
└── main.py
```

在`train.txt`和`test.txt`中存放标签：

{% code train.txt lang:text %}
./data/train/1.jpg   1
./data/train/2.jpg   1
./data/train/3.jpg   2
...
{% endcode %}

{% code test.txt lang:text %}
./data/test/1.jpg   1
./data/test/2.jpg   1
./data/test/3.jpg   2
...
{% endcode %}

**重写抽象类**

|method|function|
|------|--------|
|`__init__`|初始化成员变量，读取txt文件中的图片路径、标签等信息|
|`__getitem__`|读取单个样本数据及标签|
|`__len__`|返回数据集大小|

```python
import numpy as np
from PIL import Image
from torch.utils.data import Dataset


class MyDataset(Dataset):
    def __init__(self, txt_path, transform=None):
        self.txt_path = txt_path

        imgs = []
        with open(self.txt_path, 'r') as dp:
            for line in dp.readlines():
                line = line.rstrip()
                words = line.split()
                imgs.append((words[0], int(words[1])))

        self.imgs = imgs
        self.transform = transform

    def __getitem__(self, index):
        fn, label = self.imgs[index]
        img = Image.open(fn)
        img = np.array(img)
        if self.transform is not None:
            img = self.transform(img)

        return img, label

    def __len__(self):
        return len(self.imgs)
```

至此，一个简单的自定义数据集制作完成，调用方法与内置的数据集一般无二：

```python
import torch
from torchvision import datasets, transforms


transform = transforms.ToTensors()
train_path = r'./data/train.txt'
test_path = r'./data/test.txt'
train_data = MyDataset(train_path, transform)
test_data = MyDataset(test_path, transform)

train_loader = torch.utils.data.DataLoader(train_data, batch_size=batch_size,
    shuffle=True)
test_loader = torch.utils.data.DataLoader(test_data, batch_size=batch_size,
    shuffle=True)
```

## demo

{% btn /404.html, Download demo.zip %}