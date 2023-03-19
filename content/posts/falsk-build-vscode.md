---
title: '在VSCode中搭建Flask环境'
date: 2022-09-14
tags: [技术/python,vscode,flask]
draft: false
hideInList: false
feature: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg-blog.csdnimg.cn%2Fimg_convert%2Fe7fcf8b0b298ddb26f73d69389f0b606.png&refer=http%3A%2F%2Fimg-blog.csdnimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1666101252&t=09967d69b54e47cf0ada1dd9b717ca5a
isTop: false
---

此次学习使用 Flask ，主要是为了给爬取的数据做可视化，用 Flask 做个小网站，展示一下数据。

<!--more-->

**为什么要用Flask**

Flask 是一个轻量的 Python 框架。轻量代表着它非常的简单，核心就2个部分：
- 路由转发 Werkzeug
- 模板渲染 Jinja2

此次的网站功能比较简单，只要用模板渲染模块渲染出数据，展示出来就可以了，没有别的复杂功能，所以用 Flask 就比较合适。

**为什么要用VSCode**

VSCode是一款代码编辑软件，因为我 Python 开发也是用 VSCode，所以自然要在VSCode中搭建 Flask 环境啦。

下面是步骤。

## 先搭建python环境

见上一篇： 
{{<link "python-build-vscode">}}

## 安装flask

在当前终端输入命令 `pip3 install flask` 

*这里pip3是我电脑的pip 版本*

## 编写一个demo
```python

from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return "hello world!"

if __name__ == 'main':
    app.run()
```

## 调试

在vscode中，点击菜单【运行】>启动调试>选择Flask进行调试（或终端中运行：`python -m flask run`）

![](http://lillianwho.com/post-images/1663159578923.png)

## 成功

![](http://lillianwho.com/post-images/1663159590374.png)

## 问题汇总

### Q: pip3 安装了flask，但是import时找不到。

原因是 电脑可能存在多个python版本，flask安装到别的版本里了。解释器换成正确的版本，即可解决问题。