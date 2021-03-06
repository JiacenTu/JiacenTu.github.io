---
title:  "Python学习：Python 函数"
date: 2019-09-30 14:00:00 +0800
categories: Python
tags: Python 函数
---

> 摘要：Python 中的常见函数

## 什么是函数

函数是组织好的，可重复使用的，用来实现单一，或相关联功能的代码段。

函数能提高应用的模块性，和代码的重复利用率。你已经知道Python提供了许多内建函数，比如 print()。但你也可以自己创建函数，这被叫做用户自定义函数。

## 自定义函数

### 语法格式 

形式如下：
```python
def functionname( parameters ):
   """函数_文档字符串"""
   function_suite
   return [expression]
```

***函数的注释要写在函数名的下一行，用三个双引号包裹***

### 函数调用

示例：
```python
# 定义函数
def printme( str ):
   """打印输入的字符串"""
   print str
   return
 
# 调用函数
printme("hello world!")
printme("hello python!")
```
控制台输出：
```python
hello world!
hello python!
```

## 常见函数

### 输入输出相关函数

#### print

打印指定信息到控制台，例：
```python
print("hello python")
print("hello world")
```
控制台输出：
```sh
hello python
hello world
```

print 默认输出是换行的，如果要实现不换行需要在变量末尾加上 end=""：
```python
print("hello python", end=" ")
print("hello world")
```
控制台输出：
```sh
hello python hello world
```

通过 print 还可以格式化输出结果：

<style>
table th:first-of-type {
	width: 25%;
}
</style>

格式化字符 	| 含义
:-			| :-
%s 			| 字符串
%d 			| 有符号十进制整数，%06d 表示输出显示的位数，不足的地方用 0 补齐
%f 			| 浮点数，%.2 表示小数点后只显示两位
%%			| 输出 %

例如：
```python
name = "张三"
age = 50
high = 185.5
weigh = 65.333

print("我的名字是 %s" % name)
print("今年 %d 岁了" % age)
print("身高 %f cm" % high)
print("体重 %.2f 公斤" % weigh)

print("我的名字是 %s ，今年 %d 岁了，身高 %f cm，体重 %.2f 公斤" % (name, age, high, weigh))
```

控制台输出：
```sh
我的名字是 张三
今年 50 岁了
身高 185.500000 cm
体重 65.33 公斤
我的名字是 张三 ，今年 50 岁了，身高 185.500000 cm，体重 65.33 公斤
```

#### input

获取键盘的输入信息，用户输入的任何内容 Python 都认为是一个字符串：

语法形如 `字符串变量 = input("提示信息：")`：
```python
yourName = input("please input your name: ")
print(yourName)
```
控制台输出：
```sh
please input your name: 张三
张三
```

### 数据类型相关

#### type

#### int，float