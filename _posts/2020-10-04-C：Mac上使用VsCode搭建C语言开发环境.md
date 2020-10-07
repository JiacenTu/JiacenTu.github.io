---
layout: post
title: "Mac上使用VsCode搭建C语言开发环境"
date: 2020-10-04 14:00:00 +0800
categories: C/C++
tags: vscode 开发环境 C/C++
---

> 摘要：Mac 下使用 vscode 搭建 c 语言开发环境，以及各个配置文件的作用

> 在网上搜索各种资料时发现，各种教程和博客都有不同的地方，对于不熟悉 vscode 的人就会非常困惑。在这里强烈建议阅读：[官方文档](https://code.visualstudio.com/docs/cpp/config-clang-mac)

## 预备条件

### 环境和工具

Mac 环境下需要 Clang，可以通过以下命令查看 Clang 是否存在：

```shell
# 查看 clang 版本，如果存在，就会返回版本号
clang -v
```

如果没有，通过以下命令下载：

```shell
xcode-select --install
```

**注意**：新版的 Mac 系统例如 MacOS Catalina 在使用 `xcode-select` 时会失效，因为新版 Mac OS 已经不再自带 Command Line Tools 了，因此需要去 [Apple Developer](https://developer.apple.com/download/more/) 这里搜索下载。

### 下载

- vscode 下载：

  可以通过官网下载：[官网下载地址](https://code.visualstudio.com/)，下载后是一个压缩包，解压后就可以直接使用，也可以把它拖动到 Application 文件夹中。

- 两个插件
  - C++：如图，点击右侧最下方的按钮，然后在搜索栏搜索插件名称就好了
  - Chinese (Simplified) Language Pack for Visual Studio Code：中文包，英文好的忽略

![截屏2020-10-04 下午9.13.04](../assets/images/blog/截屏2020-10-04 下午9.13.04.png)

## 创建项目

1. 在自己的工作文件夹中创建一个项目，例如创建项目 hello
2. 使用 vscode 打开 hello 文件夹
3. 新建创建一个文件，例如 hello.cpp
4. 编写一个 Hello World ：

```c++
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main()
{
    vector<string> msg {"Hello", "C++", "World", "from", "VS Code", "and the C++ extension!"};

    for (const string& word : msg)
    {
        cout << word << " ";
    }
    cout << endl;
}
```

## 配置文件

### 为什么要使用配置文件

和平常使用的例如 VisualC++ 这类 IDE 不同的是，vscode 是一个轻量级的编辑器。可以把它理解为记事本，它没有集成环境，无法开箱即用，但通过插件拥有着强大的拓展性。所以各种的设置和配置信息都需要使用者手动添加到配置文件当中，这些配置文件告诉 vscode 如何去运行程序。

对于 C++ 而言，配置文件主要有三个：

- **c_cpp_properties.json**：指出编译器的位置
- **tasks.json**：指出如何编译这个程序
- **launch.json**：一些 debug 设置

### c_cpp_properties.json

c_cpp_properties.json 可以改变和设置一些信息。比如编译器的路径，针对哪个 C++ 标准进行编译，等等其他设置。

使用快捷键 ⇧⌘p 打开命令行面板，输入edit configurations，在弹出的列表中选择 **C/C++:Edit Configurations(JSON)**，如图所示：

![截屏2020-10-05 下午1.17.38](../assets/images/blog/截屏2020-10-05 下午1.17.38.png)

此时会自动生成 .vscode 文件，并且文件下包含 c_cpp_properties.json 文件，打开文件，内容如下：

![截屏2020-10-05 下午2.57.04](../assets/images/blog/截屏2020-10-05 下午2.57.04.png)

这个文件默认即可，只有当程序包含的头文件不在工作空间或者标准库路径时才需要修改 **includePath** 字段。

文件主要参数作用如下：

- **includepath**

  这个是程序头文件和引用库所在的路径，当它们不在工作空间或者标准库路径中时，需要添加其路径

- **macFrameworkPath**

  Mac Framework 具体并不了解，理解为一个库，包含了多种资源，用来支持程序的运行。macFrameworkPath 填写的是它的路径，默认情况无需修改

- **compilerPath**

  这是一项重要的设置，C++ 的扩展使用它来推断 C++ 标准库头文件的路径。有了它，扩展才能提供智能提示，函数定义跳转等功能。默认情况下填写的是拓展在计算机中找到的默认编译器路径。

### tasks.json

tasks.json 会告诉 vscode 如何编译程序，它将会调用 Clang C++ 编译器，把源代码编译为可执行的二进制文件。

1. 使用快捷键 ⇧⌘B 呼出命令行面板（这个快捷键相当于在命令行面板选择 Configure default build task），如图：

![截屏2020-10-05 下午10.55.02](../assets/images/blog/截屏2020-10-05 下午10.55.02.png)

2. 一直点击直到最后一步选择 Others，就会在 .vscode 文件夹下生成 tasks.json：

![截屏2020-10-05 下午10.55.26](../assets/images/blog/截屏2020-10-05 下午10.55.26.png)

将自动生成的内容用以下内容替换：

```json
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "type": "shell",
      "label": "clang++ build active file",
      "command": "/usr/bin/clang++",
      "args": [
        "-std=c++17",
        "-stdlib=libc++",
        "-g",
        "${file}",
        "-o",
        "${fileDirname}/${fileBasenameNoExtension}"
      ],
      "options": {
        "cwd": "${workspaceFolder}"
      },
      "problemMatcher": ["$gcc"],
      "group": {
        "kind": "build",
        "isDefault": true
      }
    }
  ]
}
```

**注意：**如果是 c 语言的文件可能最后编译出错如下：

```shell
error: invalid argument '-std=c++17' not allowed with 'C'
```

那么可以试试去掉这两行：

```json
# 这是要求编译使用 C++ 17
"-std=c++17",
"-stdlib=libc++",
```

Tasks.json 中主要参数意义如下：

- **label：**任务列表中出现的此次编译任务名称，随便写。
- **command：**设置了此次编译要运行的程序，在这里指定运行 Clang 编译器。
- **args：**指定了将要传递给 Clang 编译器的命令行参数，这些参数必须按照编译器所指定的顺序排列。在这个 task.json 中，args告诉了编译器，使用 C++ 17 的标准，并且编译（`-g`） 可用文件（`$file`），输出（`-o`）到当前文件夹（`${fileDirname}`），输出文件命名为 active file 的同名无后缀文件（`${fileBasenameNoExtension}`）。
- **option：**`cwd`指定当前工作目（ Current working directory ）为 hello.cpp 所在的文件夹（`${workspaceFolder}`）。
- **problemMatcher：**用于选择输出解析器，输出解析器主要用来在编译结果中查找警告和错误。对于 Clang++，使用 gcc 问题匹配器 `$gcc` 将获得最好的结果。
- **isDefault：**这个参数仅仅是为了更加方便。如果设置为 true，那么使用 ⇧⌘B 就可以直接运行这个 task；如果设为 false，仍然可以通过命令行输入 **Run build task** 来编译程序。

可以针对自己的需求对 task.json 进行更改。例如，将（`$file`）改为（`${workspaceFolder/*.cpp}`），这样就会编译工作文件夹中的所有 .cpp 文件；将（`${fileDirname}/${fileBasenameNoExtension}`）改为（`${workspaceFolder}/myProgram.out`），这样可以指定输出文件的名称。

更多变量信息可以查看：<a href="appendix">文章附录</a> 

### launch.json

launch.json

1. 使用快捷键 ⌘⇧P 呼出命令面板，输入 launch，选择 **Open launch.json**
2. 选择 **C++ (GDB/LLDB)**
3. 选择默认配置，生成 lanuch.json 内容如下：

![截屏2020-10-07 下午2.08.51](../assets/images/blog/截屏2020-10-07 下午2.08.51.png)

更改参数：

- **program**：指的是需要调试的程序名称，因此将 program 中的内容改为：

```json
 "program": "${fileDirname}/${fileBasenameNoExtension}",
```

-  **stopAtEntry**： 如果设为 true，那么在每次运行程序时，都会在 main 方法上自动打一个断点并且停在那里。

- 添加一个参数 **preLaunchTask** ：添在 **MIMode** 后面，注意逗号隔开

```json
"MIMode": "lldb",
"preLaunchTask": "C/C++: clang build active file",
```

**preLaunchTask** 表示在启动程序时，先构建程序，然后构建这个程序的名字就是 **tasks.json** 文件中的 label 参数，必须要一致，不然就不会构建程序，当然也可以手动构建程序，然后再启动程序进行调试。

## 运行和调试

### 运行

task.json 已经设置完毕，因此运行命令直接将源代码编译为可以执行文件就OK了。

1. 编译文件：

   ⌘⇧B 选择要编译的文件，vscode 会检测有哪些可编译文件，这里选择 **C/C++: clang build active file**。

   开始编译文件后，就会将编译结果输出到终端当中，如果编译成功，终端输出如图

   ![截屏2020-10-07 下午2.46.56](../assets/images/blog/截屏2020-10-07 下午2.46.56.png)

2. 生可执行文件：

   编译成功后，在 hello.cpp 所在文件夹下会自动生成可执行文件 **hello** 和调试文件 **hello.dSYM**。

3. 在终端运行可执行文件：

   ![截屏2020-10-07 下午2.58.03](../assets/images/blog/截屏2020-10-07 下午2.58.03.png)

### 调试

在代码打上断点，按下 f5 即可调试

## <a name="appendix">附录</a>

### 配置文件预定义变量含义

官方参考文档：[Variables Reference](https://code.visualstudio.com/docs/editor/variables-reference)

- **${workspaceFolder}** - the path of the folder opened in VS Code
- **${workspaceFolderBasename}** - the name of the folder opened in VS Code without any slashes (/)
- **${file}** - the current opened file
- **${relativeFile}** - the current opened file relative to `workspaceFolder`
- **${relativeFileDirname}** - the current opened file's dirname relative to `workspaceFolder`
- **${fileBasename}** - the current opened file's basename
- **${fileBasenameNoExtension}** - the current opened file's basename with no file extension
- **${fileDirname}** - the current opened file's dirname
- **${fileExtname}** - the current opened file's extension
- **${cwd}** - the task runner's current working directory on startup
- **${lineNumber}** - the current selected line number in the active file
- **${selectedText}** - the current selected text in the active file
- **${execPath}** - the path to the running VS Code executable
- **${defaultBuildTask}** - the name of the default build task