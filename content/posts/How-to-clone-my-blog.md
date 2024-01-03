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

### 修改后请重新发布
我以为不写大家也知道，看来有一点困扰哈，那我写个Notice：

大家知道hugo的发布，是要用：
```
hugo -D
```
生成静态文件到 `public` 文件夹，然后把这个文件夹上传到服务器。

上面我们修改的文件都是主题的模板文件，所以修改过后你需要重新用`hugo -D` 发布，生成新的静态文件，再将你的静态文件上传。

（如果有自动发布和上传的这个工作流，就不用管了。）

一些小伙伴修改文件后，如果发现网站没有变化，那么看看自己是不是没有重新发布。因为光修改模板文件没有用，你博客上跑的代码其实是`发布` 生成的静态文件。

希望我说清楚了。

有别的问题发邮件给我哈

(๑′ᴗ‵๑)
祝大家玩博客愉快