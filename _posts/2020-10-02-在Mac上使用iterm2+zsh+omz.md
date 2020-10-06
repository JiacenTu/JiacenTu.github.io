---
layout: post
title: "Mac上使用iterm2+zsh+Oh my zsh"
date: 2020-10-02 14:00:00 +0800
categories: 杂记
tags: itrem2 zsh ohMyzsh
---

> 摘要：通过 iterm2 + zsh + oh my zsh 来美化 Mac 上的 shell，参考链接：[iTerm2 + Oh My Zsh 打造舒适终端体验](https://zhuanlan.zhihu.com/p/37195261)。

##  为什么要使用 iterm2 和 zsh

相较于 bash，个人认为 zsh 有以下优点：

- 更加强大的 tab 补全
- 大小写自动更正
- 丰富多彩的主题
- 高亮显示

那么为什么要使用 iterm2，因为相较于系统自带终端，iterm2 支持：

- 任意窗口热键唤出（非常好用）
- 快速更改字体和主题（在设置中可以直接更换）
- 自定义命令窗口样式

附一张最终的半窗图：

![截屏2020-10-03 下午6.20.34](/Users/tjc/Pictures/md-picture/截屏2020-10-03 下午6.20.34.png)

## 下载与安装

在下载安装软件之前，需要有以下工具和环境：

- git：从 GitHub 上 Clone 项目
- Command line Tools：为 shell 提供工具（没有 Xcode 的话，新版 MacOs Catalina 不自带此工具，需要自行下载）
- pip：或者 pip3，用于下载 powerline fonts

具体安装步骤如下

### 下载安装 iterm2

可以通过官网下载：[iterm2官网](https://www.iterm2.com/)

下载完成后直接打开，注意，此时的 iterm2 还很原始，和自带终端没什么区别，接下来会通过一系列设置来美化它。

### 下载安装 oh my zsh

终端输入以下命令

```shell
# curl 安装方式
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

安装完成后会有官方提示

### 下载安装 PowerLine 和 PowerFonts

- PowerLine 安装

  PowerLine 是用 python 编写的脚本，作用是用来美化终端，安装命令如下：

  ```shell
  pip install powerline-status --user
  ```

- PowerFonts 安装

  PowerFonts 是一个字体库，里面有各种各样的字体，我们需要其中一种专用字体和 PowerLine 配合，否则终端就会出现乱码。

  安装方式使用 git 从 GitHub 克隆项目，因此需要建立一个用于存放 git 项目的文件夹，然后在此文件夹下运行命令：

  ```shell
  # git clone
  git clone https://github.com/powerline/fonts.git --depth=1
  # cd to folder
  cd fonts
  # run install shell
  ./install.sh
  ```

### 下载安装配色方案

配色方案的作用是使 shell 界面更加的美观，同时合理的配色会让 shell 观看起来更省力，否则同一个颜色不好找到想要的东西。

通过 git 克隆项目，在存放 git 项目的文件夹中运行命令，命令如下：

```shell
# git clone
git clone https://github.com/altercation/solarized
# open dir
cd solarized/iterm2-colors-solarized/
open .
```

在打开的finder窗口中，双击 Solarized Dark.itermcolors 和 Solarized Light.itermcolors 即可安装明暗两种配色。

### 下载安装主题

下载agnoster主题，在 git 项目文件夹中运行命令，命令如下：

```shell
# git clone
git clone https://github.com/fcamblor/oh-my-zsh-agnoster-fcamblor.git
# install theme
cd oh-my-zsh-agnoster-fcamblor/
./install
```

以上命令会自动将此主题拷贝到 oh my zsh 中的主题中，然后打开 zsh 配置文件，通常为 ~/.zshrc，将ZSH_THEME后面的字段改为agnoster。可以通过 vim 修改，命令如下：

```shell
vim ~/.zshrc
```

改为如图：

![截屏2020-10-03 下午10.20.46](/Users/tjc/Pictures/md-picture/截屏2020-10-03 下午10.20.46.png)

修改完后按一下 Esc，然后输入 :wq 回车一下退出 vim。然后运行以下命令使配置生效：

```shell
source ~/.zshrc
```

### 下载安装高亮插件

通过 git 下载高亮插件，命令如下：

```sh
# git clone
cd ~/.oh-my-zsh/custom/plugins/
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
# 修改配置文件
vim ~/.zshrc
```

 将 plugins 这一项添加 zsh-syntax-highlighting，并在下面加上如下一句：

```sh
source ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```

修改后如图所示：

![截屏2020-10-03 下午10.28.57](/Users/tjc/Pictures/md-picture/截屏2020-10-03 下午10.28.57.png)

然后退出 vim。

最后运行以下命令使配置生效：

```shell
source ~/.zshrc
```

### 修改 iterm2 配置

最后一步就是修改 iterm2 配置，让他更好用。

打开 iterm2，Command + O 打开 Profiles 如下图：

![截屏2020-10-03 下午10.35.32](/Users/tjc/Pictures/md-picture/截屏2020-10-03 下午10.35.32.png)

点击 Edit Profiles

在 Color -> Color Presets 中根据个人喜好选择刚刚下载好的配色方案：

![截屏2020-10-03 下午10.47.01](/Users/tjc/Pictures/md-picture/截屏2020-10-03 下午10.47.01.png)

在 Text -> Font 中搜索 Meslo LG 字体，有L、M、S可选，看个人喜好：

![截屏2020-10-03 下午10.45.08](/Users/tjc/Pictures/md-picture/截屏2020-10-03 下午10.45.08.png)

在 Window 中可以设置透明度，背景图，打开方式。

在 Keys -> Hotkey Window -> Configure Hotkey Window -> Hotkey 可以设置唤出热键。

在 Window -> space 选择 All space 就可以在任意窗口唤出 shell 了。