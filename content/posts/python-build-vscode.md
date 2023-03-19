---
title: '在VSCode中搭建Python开发环境'
date: 2022-09-14
tags: [技术/python,vscode]
draft: false
hideInList: false
feature: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg.cnpython.com%2Fmedia%2Findex%2Ft1.png&refer=http%3A%2F%2Fimg.cnpython.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1666101121&t=c8d943c088b543522c769b286a8a4d8d
isTop: false
---

本文是一篇在vscode中搭建python开发环境的教程。

VSCode（全称：Visual Studio Code）是一款免费的代码编辑器。进行 Python 开发时最经典的IDE应该是PyCharm（JetBrains公司出品），但是 JetBrains 系的软件都要收费，VSCode 的优点在于免费、通过插件可以支持多种语言的代码编辑，是一款非常强大的软件。


<!--more-->


本文阅读前提为：
1. 已安装python
2. 已安装vscode


## 步骤

1. 打开VSCode， 安装python扩展
2. 新建一个文件夹，并在VSCode 中打开
3. 搭建虚拟环境(venv)。教程见下文
4. 指定解释器。教程见下文

虚拟环境和解释器都配置好之后，环境就搭建好了，可以进行开发与调试(debug)了。

### 搭建python虚拟环境

即安装 env。

1. 安装virtualenv

在当前项目窗口下，终端>新终端，并输入一下命令。等待安装成功。

`pip3 install --user virtualenv`

*注意：用pip命令还是pip3命令，要看自己使用的是pip版本，一般来说，python3自带的是pip3*

2. 运行：`python3 -m venv env` 。当前项目下会多出env文件夹，即证明虚拟环境搭建成功。

[No module named venv问题的出现和解决](https://blog.csdn.net/qq_39453977/article/details/103088426)

### 指定解释器

vscode：查看-命令面板-输入选择：Python：Select Interpreter 选择解析器

