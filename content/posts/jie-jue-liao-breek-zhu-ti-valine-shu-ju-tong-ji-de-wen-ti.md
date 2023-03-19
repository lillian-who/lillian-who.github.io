---
title: '解决了Breek主题Valine数据统计的问题'
date: 2022-09-23
tags: [折腾]
draft: false
hideInList: false
feature: 
isTop: false
---
Breek 主题自带了 Valine 系统，并且可以开启阅读统计，开启后会在首页以及文章页面显示单个文章的评论数和阅读数。

但是，我使用过程中发现这两个数字都是0，不会被更新。一直以为是 LeanCloud 函数的问题，今天查看请求的时候，发现了问题所在。

<!--more-->


文章详情页下，获取评论数的请求，总共请求了2次。

一次请求参数是这样的，返回数据评论数是正常的。
```
where: {"$or":[{"rid":{"$exists":false}},{"rid":""}],"url":"/post/a-book-that-make-you-want-to-share/"}
```

一次是这样的，返回值为0：
```
 where: {"$or":[{"rid":{"$exists":false}},{"rid":""}],"url":"/a-book-that-make-you-want-to-share/"} 
```

对比两个请求参，发现不同之处是 url 参数。也就是说当前代码里面给定的 url 获取值不对。

把 post.ejs 里面 xid 的值，加上 `/post`，修改后如下：
```html
<i class="fa fa-comment remixicon"></i><span class="comment-count valine-comment-count" data-xid="/post/<%= post.fileName %>/"> </span>
```

测试，文章页可以正常显示评论数了。

把阅读数量的 data-xid 也改为带 `/post` 的格式，把首页也一样操作。问题解决。

---
想给 Breek 的github 提交 Pr ...... 