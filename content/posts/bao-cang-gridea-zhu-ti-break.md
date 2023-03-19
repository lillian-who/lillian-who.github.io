---
title: '宝藏Gridea主题：Break'
date: 2022-09-19
tags: [折腾]
draft: false
hideInList: false
feature: https://s2.loli.net/2022/09/19/ngqE6uR83Jm1FrK.png
isTop: false
---
事情始于我给博客找可用的评论系统。


之前我是用hexo建站的，使用了Twikoo 当评论系统，体验非常好。在此也感谢从那时起就给我博客评论和留言的人，真的给我的写博客之路很大的支持，让我不是在单机写作。

自从给网站备案以后，评论就因为备案原因关闭了。看了下日期，那是2022-02-25，原来我已经单机写作这么长时间了。于是突发奇想，想冒险把评论打开。

我当前使用的博客系统是 [Gridea](https://gridea.dev)。推荐想写博客的人尝试这个工具，操作简单，发博客也简单，技术门槛很低。

但现在美中不足的是， Gridea支持的评论系统只有 Gitalk 和 Disqus ，这两款评论系统对国内的支持都不太好，我一顿操作下来把 Gitalk 配置好了，但是接口 403，显示网络错误，这就很emo了。

在 Gridea 的github 主页找评论系统相关的信息，并提交了一个 issues 希望开发者能支持 Twikoo 之后，忽然看到有一个issues 提到 [Valine 评论系统](https://valine.js.org)，同时有一个主题链接。让我打开了新世界的大门。

就是它：
![](https://s2.loli.net/2022/09/19/ngqE6uR83Jm1FrK.png)

Gridea 目前的主题还是不多的，官网主题页面都不用翻页（没有多到需要翻页的意思），而这个主题，因为预览的链接已经失效了，所以以为已经挂了，没想到顺着链接进入了主题的github 主页，抱着试试看的想法，下载下来。

换上的一瞬间，我升华了。给大家看一下效果：

![](http://lillianwho.com/post-images/1663521958407.gif)

也太好看了吧！

我的博客素了这么久，猛然间看到这种主题才发现：啊！我还是好喜欢这种多彩的主题。

这个主题带了 [Valine](https://valine.js.org)，把 [LeanCloud](https://console.leancloud.cn/apps)  里生产的ID和秘钥填写进自定义配置下的 Valine 评论配置，保存即可（如何获取AppID和AppKey详见[Valine 快速开始](https://valine.js.org/quickstart.html)）。就是现在你能在网上看到的效果啦~

在文章页的下方，有一个评论框，只用填写一个昵称就可以评论啦~ 欢迎给我留言

![](https://s2.loli.net/2022/09/19/4bCRscADZMLBlv3.png)

---
## 致谢

最后，感谢开发者写出这么好看的主题！以及感谢 Gridea 的作者，开发出这么好用又免费的博客客户端。感恩 Thanks♪(･ω･)ﾉ

- [Gridea 一个静态博客写作客户端](https://gridea.dev)：一个用于写静态博客的客户端，源文件是md，如果创作者本身就是用md写作的话，导入以前作品列表就很方便。相比于hexo的命令操作模式，Gridea的客户端界面操作对用户很友好。
- [Breek 主题](https://github.com/lmm214/gridea-theme-breek/) ：Gridea 的一款主题
- [Valine 评论系统](https://valine.js.org) ：一个简单的评论系统，简单在引入使用非常容易，本身也非常轻量。无后端，用户评论时不需要登录。
- [LeanCloud](https://console.leancloud.cn/apps)  ：云引擎+数据库，用于托管静态网站 。此处使用它部署Valine，只用新建一个免费应用，拿到应用ID和秘钥就可了，不需要更多的云开发知识。