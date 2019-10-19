---
title:  "Python学习：Python 语法"
date: 2019-09-29 14:00:00 +0800
categories: Python
tags: Python 语法
---

> 摘要：Python 的语法规则

## 注释

### 单行注释

单行注释用 # ，# 后一行的内容视为注释：
```python
# 注释：价格为100
price = 100 
```

### 多行注释

多行注释使用三个连续的单引号或者双引号为开始，再次三个连续的单引号或双引号为结束，中间内容视为注释：
```python
""" 
注释：
价格为100
"""
price = 100 
```

## 行和缩进

### 缩进

学习 Python 与其他语言最大的区别就是，Python 的代码块不使用大括号 {} 来控制类，函数以及其他逻辑判断。Python 最具特色的就是用缩进来写模块。

***缩进的空白数量是可变的，但是所有代码块语句必须包含相同的缩进空白数量，这个必须严格执行。***

### 空行

函数之间或类的方法之间用空行分隔，表示一段新的代码的开始。类和函数入口之间也用一行空行分隔，以突出函数入口的开始。

空行与代码缩进不同，空行并不是Python语法的一部分。书写时不插入空行，Python解释器运行也不会出错。但是空行的作用在于分隔两段不同功能或含义的代码，便于日后代码的维护或重构。

## 标识符

标识符就是程序员定义的函数名，变量名

### 命名规则

* 标识符由字母、数字和下划线组成
* 不能用数字开头
* 标识符对大小写敏感

### Python 保留字

保留字即关键字，我们不能把它们用作任何标识符名称。Python 的标准库提供了一个 keyword 模块，可以输出当前版本的所有关键字：

```python
import keyword
print(keyword.kwlist)
```
控制台输出：
```sh
['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

## 变量赋值

Python 中定义变量不需要指定变量类型，定义变量语法格式形如 `变量名 = 变量值`：
```python
# 给一个变量赋值
num_int = 123 

# 多个变量赋值
a = b = c = 1

# 多个变量赋多个值
a, b, c = 1, 2, "runoob"
```

## 变量计算

### 数字型变量

Python 中数字型变量是可以直接计算的，`布尔类型 True 视为 1，False 视为 2`：
```python
isTrue = True
isFalse = False 

num_int = 100
num_float = 3.5

print(num_int + isTrue) # 101
print(num_int + isFalse) # 100

print(num_float * isTrue) # 3.5
print(num_int * isFalse) # 0
```

### 字符串拼接

字符串可以通过 `+` 进行拼接，也可以通过 `*` 拼接多次：
```python
first_Name = "张"
last_Name = "三"

# 通过 + 拼接
print(first_Name + last_Name) # 张三

# 通过 * 拼接多次
print(first_Name * 3) # 张张张
```

***注意：Python 中字符串不能和数字类型变量进行计算***

## if 语句

### 单一情况：if else

示例：
```python
langue = "python"

if langue == "python":
    print("hello python")
else:
    print("hello world")
```
控制台输出：
```sh
hello python
```

### 多种情况：if elif

示例：
```python
langue = "java"

if langue == "python":
    print("hello python")
elif langue == "java":
    print("hello java")
elif langue == "c":
    print("hello c")
else:
    print("hello world")
```
控制台输出：
```sh
hello java
```

## while 语句

```python
while condition:
    statements
```

```python
# 九九乘法表
row = 1

while row <= 9:
    col = 1
    while col <= row:
        print("%d * %d = %d" % (col, row, col * row), end="\t")
        col += 1
    print("")
    row += 1

```
控制台输出：
```sh
1 * 1 = 1	
1 * 2 = 2	2 * 2 = 4	
1 * 3 = 3	2 * 3 = 6	3 * 3 = 9	
1 * 4 = 4	2 * 4 = 8	3 * 4 = 12	4 * 4 = 16	
1 * 5 = 5	2 * 5 = 10	3 * 5 = 15	4 * 5 = 20	5 * 5 = 25	
1 * 6 = 6	2 * 6 = 12	3 * 6 = 18	4 * 6 = 24	5 * 6 = 30	6 * 6 = 36	
1 * 7 = 7	2 * 7 = 14	3 * 7 = 21	4 * 7 = 28	5 * 7 = 35	6 * 7 = 42	7 * 7 = 49	
1 * 8 = 8	2 * 8 = 16	3 * 8 = 24	4 * 8 = 32	5 * 8 = 40	6 * 8 = 48	7 * 8 = 56	8 * 8 = 64	
1 * 9 = 9	2 * 9 = 18	3 * 9 = 27	4 * 9 = 36	5 * 9 = 45	6 * 9 = 54	7 * 9 = 63	8 * 9 = 72	9 * 9 = 81	
[Finished in 0.0s]
```

## for 循环

### 普通 for 循环

for 循环可以遍历任何序列的项目，如一个列表或者一个字符串，语法格式如下：
```python
for iterating_var in sequence:
   statements(s)
```
例如：
```python
for letter in 'Python':     # 第一个实例
   print '当前字母 :', letter
 
fruits = ['banana', 'apple',  'mango']
for fruit in fruits:        # 第二个实例
   print '当前水果 :', fruit
 
print "Good bye!"
```
控制台输出：
```sh
当前字母 : P
当前字母 : y
当前字母 : t
当前字母 : h
当前字母 : o
当前字母 : n
当前水果 : banana
当前水果 : apple
当前水果 : mango
Good bye!
```

### for else

使用 for ... else ... 时，如果没有使用 break 跳出 for 循环，else 语句内容就会执行：

```python
a = [0, 1, 2, 3]

for x in a:
    print(str(x) + " ", end="")
    if x == 2:
        break
else:
    print()
    print("else 语句内容")
```
控制台输出：
```sh
0 1 2 
```

```python
a = [0, 1, 2, 3]

for x in a:
    print(str(x) + " ", end="")
else:
    print()
    print("else 语句内容")
```
控制台输出：
```sh
0 1 2 3 
else 语句内容
```

## 运算符

### 算数运算符

<style>
	table th:nth-child(1)
	{
		width: 15%;
	}
</style>>

符号 	| 含义 			| 实例
:-:		| :-:			| :-:
+		| 加				| 10 + 20 = 30
-		| 减				| 20 - 10 = 10
*		| 乘				| 10 * 10 = 100
/		| 除				| 50 / 10 = 5
//		| 取整数			| 20 / 15 = 1
%		| 取余数			| 20 % 15 = 5
**		| 幂				| 3 ** 2 = 9

### 逻辑运算符

* and
	
与，同真为真：

```python
langue = "python"
flag = True

if langue == "python" and flag == False:
    print("hello python")
else:
    print("hello world")
```
控制台输出：
```sh
hello world
```

* or

或，同假为假：

```python
langue = "python"
flag = True

if langue == "python" or flag == False:
    print("hello python")
else:
    print("hello world")
```
控制台输出：
```sh
hello python
```

* not

非，结果相反：
```python
flag = True

if not flag == False:
    print("hello python")
else:
    print("hello world")
```
控制台输出：
```sh
hello python
```

## 可变类型与不可变类型

不可变数据类型： 当该数据类型的对应变量的值发生了改变，那么它对应的内存地址也会发生改变，对于这种数据类型，就称不可变数据类型。

可变数据类型 ：当该数据类型的对应变量的值发生了改变，那么它对应的内存地址不发生改变，对于这种数据类型，就称可变数据类型，当可变数据类型改变时它实际上是更改了内存中的内容。

### 可变类型

* 数字
* 字符串
* 元组

### 可变类型

* 列表
* 字典
