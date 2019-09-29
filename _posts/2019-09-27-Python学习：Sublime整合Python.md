---
title:  "Python学习：Sublime text3 配置 python"
date: 2019-09-27 14:00:00 +0800
categories: Python
tags: Python SublimeText3
---

> 摘要：Mac 环境下使用 Sublime text3 整合配置 Python 运行环境

## Sublime text3

这是一款优秀的代码编辑器，支持多种编辑语言。

以前使用过 Pycharm ，说实话， Pycharm 确实非常强大，功能齐全。但是功能太多了，多到绝大部份根本使用不上，这时候就显得比较笨重。而 Sublime 相对来说就十分轻量级了，秒启动，而且插件极多，可以根据需要选择需要的功能。

## Python 设置

按照以下步骤设置

### 新建 Build System

在上方菜单栏点击 Tools，点击 Build System，点击最下方的 New Build System，然后将自动生成的内容替换如下内容：
```json
{
	"cmd": ["/Users/xxx/.pyenv/versions/vtl-374/bin/python3", "-u", "$file"],

}
```
其中 /Users/xxx/.pyenv/versions/vtl-374/bin/python3 是 Python 的路径，注意是 bin 目录下的，也可以指定成虚拟环境的路径。

然后保存，名字随便取，但是后缀不要错，后缀为 .sublime-build

### 使用 Build System

在上方菜单栏点击 Tools，点击 Build System，然后选中刚刚新建的 Build System。

然后在上方菜单栏点击 View，单机 Syntax，选择 Python。

### 运行

新建文件 hellopython.py ，输入代码：
```python
print("hello python")
```
点击 Command + B 运行程序，输出结果如下：
```sh
hello python
[Finished in 0.0s]
```

## 常用 Python 插件

为了更加高效地使用 Sublime text3，需要以下几个常用插件

### Package Control

#### 作用

管理 Sublime text3 的插件，能够下载，卸载，列出插件。

#### 使用方式

Command + shift + p 调出命令窗口：

<style>
table th:first-of-type {
  width: 20%;
}
</style>

输入 	| 选择 									| 作用
:- 		| :-									| :-
install | Package Control：Install Package		| 在新出现窗口中输入想要下载的插件名称就可以下载插件
remove 	| Package Control：Remove Package		| 在新出现列表中选择想要卸载的插件就可以卸载插件
list	| Package Control：List Package			| 列出所有已经安装的插件

### Terminus

#### 作用

能够在 Sublime text3 内部打开命令窗口。

#### 使用方式
	
Command + shift + p 调出命令窗口，输入 open：

<style>
table th:first-of-type {
  width: 40%;
}
</style>

选择 									| 作用
:-										| :-
Terminus: Open Default Shell in Panel	| 在下半部分以面板的形式打开一个命令窗口
Terminus: Open Default Shell in View	| 打开一个新的页面作为命令窗口

### SublimeREPL

#### 作用

* 打开交互式窗口
* 调试程序

#### 使用方式

* 打开交互式窗口

例如 input 等函数需要与键盘输入进行交互时，仅仅 Command + b 是无法进行输入的，需要打开交互式环境。点击 Preferences -> Key Bindings 输入以下内容：
	
```json
{ 
	"keys": ["f5"], "caption": "SublimeREPL:Python", 
	"command": "run_existing_window_command", "args":
  	{
       "id": "repl_python_run",
       "file": "config/Python/Main.sublime-menu"
  	} 
}
```

Command + b 运行程序，然后点击 F5 就会打开交互式环境。

* 调试程序

