---
title: obsidian配合hugo、cloudflare：让发布博客简单到不可思议
tags: [折腾,博客]
date: 2023-03-11
draft: false
hideInList: false
isTop: false
feature: 
---

![image.png](https://s2.loli.net/2023/03/18/WzmvgDcoRysPAhi.png)

自从我更换博客系统到 hugo 之后，我越来越少发博客了。原因除了最近写得少之外，就是发布起来不如之前使用 Gridea 那么方便了。

参考了几篇文章，现在的发布流程为：
1. obsidian 创建文章并写作。
2. 利用 obsidian-git 插件将文件自动同步到 github
3. cloudflare 自动拉取 github 仓库，并自动构建为hugo 项目，相当于省略了本地执行 `hugo -D` 的过程。

<!--more-->

旧的发布方式为：
1. obsidian中写作文章
2. 复制文件到 hugo 项目的 content/posts 文件夹
3. 然后执行 hugo -D 命令，生成静态文件
4. 再到public 文件夹下使用 git 将已生成的静态文件上传到 github。github page 作为博客展示。

这个过程是非常麻烦的。

今天看到木木的博客中提到的 Cloudflare，就想着改造一下。改造过程如下。

### 使用到的 obsidian 插件

#### image auto upload plugin

用于自动上传图片到图床。需要配合 picgo 使用。

#### quickadd

用于快速创建一篇新博客。

下面是我的设置：

1. 创建一个 `Template` 类型的quickadd 命令

![image.png](https://s2.loli.net/2023/03/11/HXaVj2uZneSE9l6.png)

2. 在根目录新建一个 `_Templates` 文件夹，并创建模板文件 `hugo博客模板`
```
---
title: {{NAME}}
tags: [{{VALUE:tag？}}]
date: {{DATE:YYYY-MM-DD HH:mm:ss}}
draft: true
hideInList: false
isTop: false
feature: 
---
```

published 字段是发布，默认设置为false，草稿。等到文章写完并修改无误后，再修改为 true 进行发布。


4. 设置quickadd 命令：
![image.png](https://s2.loli.net/2023/03/11/Z9BDtVHJr2uaIyq.png)

#### obsidian-git

用于自动备份文件到 github。

插件设置修改如下：
![image.png](https://s2.loli.net/2023/03/11/cxTJiutPEfkHFW8.png)

### 启用 Cloudflare 

打开 [Cloudflare Dash](https://dash.cloudflare.com/) 导航栏 `Pages` ，点 `创建项目`，授权 Github 项目，选择博客所在仓库，选择正确的分支。

添加环境变量，指定高版本 `HUGO_VERSION` 为 `0.92.0`

然后部署即可。

部署完成后就可以使用 cloudflare 的二级域名访问博客了。如果你像我一样有自己的独立域名，那么可以进行域名绑定。

###  Cloudflare 绑定独立域名

首先第一步，把自己的域名托管到 cloudflare。参考： [如何将域名托管到cloudflare](https://www.back2me.cn/skills/cloudflare.html) 这篇文章。

然后打开导航栏 Pages ，在右侧找到刚刚的博客站点，在设置或者部署中找到 【自定义域】，设置自定义域名，输入之前托管进来的域名，按照指引完成绑定。

![image.png](https://s2.loli.net/2023/03/11/mToq84ZpMhFjyGN.png)

以上，所有设置都已完成。

现在我要发布一篇新博客时，只要在 obsidian 中打开 hugo博客的这个库，然后使用 quickadd 新建一篇博客，写上内容，然后把yaml 中的 `published`  字段值改为 `true` 即可（从草稿改为发布）。等待3分钟后 obsidian-git 插件自动同步到 github，博客就自动更新发布好了。

这篇文章就是使用新方式发布的，优雅不是一点点。

### 参考

- 木木木木木： [Hugo With Obsidian](https://immmmm.com/hugo-with-obsidian/) 
- 木木木木木： [Hi , Cloudflare Pages](https://immmmm.com/hi-cloudflare/)
- [Hugo 博客写作最佳实践](https://blog.zhangyingwei.com/posts/2022m4d11h19m42s28/)
- [如何将域名托管到cloudflare](https://www.back2me.cn/skills/cloudflare.html)