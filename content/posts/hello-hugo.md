---
title: "Hello Hugo"
date: 2022-10-18
tags: [折腾]
draft: false
hideInList: false
feature: 
isTop: false
---


![](https://s2.loli.net/2022/10/18/zIW2G7T4FldPCy8.png)

## 为什么换hugo？

纯粹是喜欢 [木木的博客](https://immmmm.com/)，想要像他一样**在文章列表里面显示丰富的文章内容**。在gridea里没有找到心仪的主题，干脆折腾一下，搞个hugo 的 demo 看一下。

地址：http://hugoblog.lillianwho.com/

<!--more-->

## 一些特殊语法

### 站内链接美化

```
{\{<link "文章文件名">}\}
```

*去掉反斜杠*

效果：


![](https://s2.loli.net/2022/10/18/fMReN1xkUgE7jSW.png)

### 文章内豆瓣读书卡片

直接放豆瓣的链接
```
<https://book.douban.com/subject/26315455/>
```

效果：

![](https://s2.loli.net/2022/10/18/syV9YzfHSZgk852.png)


## 踩坑

- 正如木木所说，yaml 里面的date 只能统一格式，要么是带时区的格式，要么就`年-月-日`，文章比较多，改日期花了点时间
- Twikoo，我用的是木木折腾好的主题，Twikoo 评论已经内置了，然而，一通操作下来终于重新部署好了，忽然发现 vercel 国内访问直接死掉。。。呵呵，我也死了。所以最后忍痛关掉了评论。

## 大家可能关心的问题

### RSS

地址是  域名/atom.xml

### 多出来的博客怎么办

hugo站当前（2022-10-18这一天）只作为 demo 尝个鲜。我自己是很心动的，觉得阅读体验比较好，后期考虑把这个站点解析到主域名，不会让大家再保存一个域名的。

hugo 比 Gridea 所欠缺的是，没法（也不是没办法，只是比较麻烦）一键部署到私有服务器。如果后续直接发布到 github page，那就没啥问题了，不然每次手动更新文章，要累死了。Gridea 配置过后，不管是发布到 github page 还是私有服务器，都非常方便。写作也有独立的客户端界面，发布按钮也是可视化的，相对来说更人性化，更省心。

这次更新最主要是为了首页的文章列表的显示。文章内的内容所见即所得的显示在列表上，看起来就非常舒服，是 Gridea 里的主题显示摘要所达不到的效果。

### 参考

- 木木的博客：[Hello, hugo](https://immmmm.com/hello-hugo/)