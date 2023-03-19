---
title: '用docsify生成文档网站'
date: 2022-09-21
tags: [折腾]
draft: false
hideInList: false
feature: https://s2.loli.net/2022/09/21/EKr6bulWe31mRMq.png
isTop: false
---

docsify 是一个文档网站生成器。把你的 markdown 文件扔进去，它会生成文档型的网站。


<!--more-->


[docsify 文档](https://docsify.js.org/)

从[林木木](https://github.com/lmm214) 的博客文章 [Hi,Docsify](https://immmmm.com/hi-docsify/) 中处得知docsify。他用 docsify 做了小学学科的教学辅助。(林木木是我现在使用的 Breek 主题的作者)

网友的网站：
-  [sosilent的个人学习库](https://doc.sosilent.top/#/)
	- ![](https://s2.loli.net/2022/09/21/W9VZyxcSHi3zUnI.png)

- 林木木的 [小学语文教学助手](https://edui123.com/ebook/xxyw/#/)
	- ![](https://s2.loli.net/2022/09/21/j4YPvEgMKuCid6Q.png)

所以就很心动，想要尝试一下，正好我觉得一些分章节的教程用博客文章的形式展现不太好。想要一个以 「项目-章节」的形式展现。下面开始动手。

## Hello , docsify

### 第一步：全局安装 `docsify-cli` 工具

可以方便地创建及在本地预览生成的文档。

```bash
npm i docsify-cli -g
```

第一步就失败了...

![](https://s2.loli.net/2022/09/21/gPdsJjZRoKYe8vS.png)

看报错，原因是没有文件夹权限（上网搜索了下基本确定是没有权限），加个sudo继续

```bash
sudo npm i docsify-cli -g
```

执行。提示输入密码，输入电脑密码后回车，执行成功。

### 第二步：初始化项目

新建一个文件夹，或者在你想要写文档的项目文件夹里，执行命令：

```bash
docsify init ./docs
```

![](https://s2.loli.net/2022/09/21/kTdsuQGOZABCViY.png)

### 第三步：写文档

docs文件夹下的Readme.md 会作为主页渲染，所以直接把文档内容写进readme。

我把之前写的python 爬虫爬取豆瓣的学习笔记放上去了。

![](https://s2.loli.net/2022/09/21/M8zpAr7BG5qWvmi.png)

执行命令渲染：

```bash
docsify serve ./docs
```



打开 http://localhost:3000/ 看到渲染完成的页面如下：

![](https://s2.loli.net/2022/09/21/ltoA28sbBP4fEHr.png)

至此，官方的start 就走完了。Docsify 版「Hello ,world !」搞定！

接下来，增加需求：
- 网站放多个项目：这个文档网站，我的定位是放上我所有的学习笔记和文档。尤其是那些用一篇文章结束不了的。
- 一个项目分多章节：比如python 爬虫和数据分析这个项目，会分为爬虫和数据分析两个大章节。分为不同的章节可以让阅读体验更好。
- 我想要上方导航栏，用于区分不同的项目。还要增加一个菜单，用于导航到我的博客主页，打通博客与文档网站。
- 增加主页

## pro

### 多项目

在./docs 下面新建文件夹，按文件夹来区分项目。我这里有2个项目，`obsidian 指南`和`python爬虫与数据分析`，所以我建了2个文件夹。

项目入口放在上方导航栏，所以我们来定制一下导航栏。

### 定制导航栏

在 index.html 文件里，找到 `window.$docsify` ，添加两行代码。

```html
 // 开启自定义导航
  loadNavbar: true,

  // 指定加载 nav.md
  loadNavbar: 'nav.md',
```
![](https://s2.loli.net/2022/09/21/XGK5NzEvScpjeqV.png)


我的 nav.md里是这样写的：

```md
* [首页](/)
* [python爬虫与数据分析](/python爬虫与数据分析/)
* [obsidian指南](/obsidian指南/)
* [Blog](http://lillianwho.com)
```

注意：`/python爬虫与数据分析/` 地址导向 `/python爬虫与数据分析/README.md`


效果如下：

![](https://s2.loli.net/2022/09/21/7rP5O8JRGZMhpeK.png)



### 定制左侧边栏

`/python爬虫与数据分析` 文件夹下有2个文档，也就是我要分的2个章节：
- Readme.md ：放爬虫的教程
- 数据分析.md ：放爬取数据后数据分析的相关教程。（也可以分得更细）

想要在一个项目下，看到每个文档，以及把每个文档下的二级标题展示出来，也就是要做成嵌套边栏。当我访问python爬虫这个项目的时候，要只看到这个文件夹下自己的侧边栏。

那么就在 `/python爬虫与数据分析` 文件夹建一个 `_sidebar.md`，表示加载这个目录自己的侧边栏。

`/python爬虫与数据分析/_sidebar.md` 里填写：

![](https://s2.loli.net/2022/09/21/3ZFxpIhkB2MKGsn.png)



在`/index.html` 的 `window.$docsify` 里添加：

```
 // 定制左侧边栏
      loadSidebar: true,
      subMaxLevel: 2  #表示显示文件目录
```

这样在访问 `python爬虫与数据分析` 项目时，左侧边栏就能看到项目下的2个文件，并且展开了文件目录。

![](https://s2.loli.net/2022/09/21/3wmXst5Cd6zMhGJ.png)


接下来用同样的方法，设置 `obsidian指南` 项目。


### 首页

建一个 `_coverpage.md` ，这个名称是默认的封面名。

![](https://s2.loli.net/2022/09/21/wJGqaidC47eXpEQ.png)

在 `index.html` 里设置 `coverpage` 参数，可以开启渲染封面的功能。

```html
<script>
  window.$docsify = {
    coverpage: true,
    onlyCover: false,  // 将封面作为首页，访问 `/`根目录时，不再显示readme的内容，而是显示封面
  }
</script>
```
效果如下：

![](https://s2.loli.net/2022/09/21/EKr6bulWe31mRMq.png)


## 部署

只要把文件原样上传，把访问指向docs文件夹即可。至于上传到自己的服务器，还是github无所谓。

以宝塔为例，在文件菜单，新建了一个 docsify文件夹来放文档，把`docs` 文件夹原样上传。

![](https://s2.loli.net/2022/09/21/RTmiyzpoBjKXJ6a.png)

然后在 `网站` 菜单，添加一个站点，用二级域名 `docs.lillianwho.com` 指向了 该文件夹

![](https://s2.loli.net/2022/09/21/XnBYKtpW7zEFHSd.png)

最后，到域名服务商那里，添加一条DNS解析

![](https://s2.loli.net/2022/09/21/1cwZKqoFk4BaXU5.png)

完成！

文档网站地址：http://docs.lillianwho.com/

现在，把这个网址添加到博客的导航，即可达到两个网站互通的效果。

![](http://lillianwho.com/post-images/1663707180350.gif)