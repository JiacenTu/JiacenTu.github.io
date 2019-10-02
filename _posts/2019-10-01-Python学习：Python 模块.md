---
title:  "Python学习：Python 模块"
date: 2019-10-01 14:00:00 +0800
categories: Python
tags: Python 模块
---

> 摘要：Python 模块相关概念

## Python 模块

### 什么是 Python 模块

Python 模块(Module)，是一个 Python 文件，以 .py 结尾，包含了 Python 对象定义和Python语句。

### 为什么要使用模块

* 模块让你能够有逻辑地组织你的 Python 代码段。
* 把相关的代码分配到一个模块里能让你的代码更好用，更易懂。

类似于 Java 中的类

## 使用 Python 模块

### import 语句

模块定义好后，我们可以使用 import 语句来引入模块，语法如下： 

```python
import module1
import module2
import module3
```

### from import 语句

Python 的 from 语句让你从模块中导入一个指定的部分到当前命名空间中。语法如下：
```python
from modname import name1
```

### 调用函数

引用模块后，就可以调用模块中的函数了，调用语法如下：
```python
模块名.函数名
```

例：
```python
import random

for i in range(10):

    print(random.randint(1, 10))
```
控制台输出：
```sh
3
1
8
2
7
1
1
10
1
1
```

### 模块名也是标识符

每一个 python 文件都是一个模块，所以每一个文件名应该遵循标识符命名规则

## Python 模块搜索路径

当你导入一个模块，Python 解析器对模块位置的搜索顺序是：

1. 当前目录
2. 如果不在当前目录，Python 则搜索在 shell 变量 PYTHONPATH 下的每个目录。
3. 如果都找不到，Python 会察看默认路径。UNIX 下，默认路径一般为 `/usr/local/lib/python/`。

模块搜索路径存储在 system 模块的 sys.path 变量中。变量里包含当前目录，PYTHONPATH和由安装过程决定的默认目录。