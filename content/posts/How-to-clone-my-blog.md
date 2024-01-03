---
title: 如果你也想拥有我的同款博客
tags:
  - 折腾
date: 2024-01-03 15:43:28
UID: 20240103154328
draft: false
toc: false
feature:
---

近期我收到好几个不属于我博客的评论通知邮件，点击链接发现了新的小站。看来大家都挺喜欢我的博客的哈，我不敢自专，博客主题是[木木](https://immmmm.com)的，我只对页面做了很小的改动。

这个主题真是广受喜爱，我自己也是粉丝的一员。木木老师牛逼！赞美木木老师！

可能因为一些原因，大家想要和我博客一模一样的效果，所以拉取了我的整个库。这也没有问题，但是你还需要做以下事情：
<!--more-->
### 修改评论账号

评论是使用的Twikoo，请参考[Twikoo中文文档](https://twikoo.js.org/)。不是开箱即用哈，你需要去**部署**自己的Twikoo，然后把主题模板里的 twikoo `envId` 更换为自己的。

需要修改的文件在：
```
/themes/hello-frend/layouts/partials/comments.html
```

和

```
/themes/hello-frend/layouts/_default/twikoo.html
```

记不住也可以在`/themes/hello-frend/layouts` 里搜索 `envId` .

如果你暂时没有搞定Twikoo的部署，可以在根目录的 `config.toml` 文件，找到最下方的twikoo设置项，把 `enable` 的值改为 false，暂时关闭评论。

P.S 站点地址和站点名称、目录，也是在`config.toml` ，可能大家一看这个文件就能知道了，所以不用我多说。
### 更换或关闭newsletter 订阅

文章下方有个邮件订阅功能，这个是用 Tinyletter 做的，之前有发过文章，大家可以去参考。这个也是填了我的账号，有人点击订阅也会订阅到我的频道，而不是你们自己的博客。

要删除这个模块，在 `/themes/hello-frend/layouts/_default/single.html`模板，第91行：
```
//删除这句
{{ partial "subscribe-form.html" . }}
```
如果你搞定了自己的tinyletter流程，可以把自己的地址填进来，在
```
/themes/hello-frend/layouts/partials/subscribe-form.html
```

把`https://tinyletter.com/lillianwho` 替换为你自己的链接。

---

暂时就想到这两个。

祝大家玩博客愉快