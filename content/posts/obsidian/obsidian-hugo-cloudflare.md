---
title: obsidian+hugo+cloudflare自动发布博客
tags: [折腾,博客]
date: 2023-03-11
published: true
hideInList: false
isTop: false
feature: 
---

自从我更换博客系统到 hugo 之后，我越来越少发博客了。原因除了最近写得少之外，就是发布起来不如之前使用 Gridea 那么方便了。

参考了几篇文章，现在的发布流程为：
1. obsidian 创建文章并写作。
2. 利用 obsidian-git 插件将文件自动同步到 github
3. cloudflare 自动拉取 github 仓库，并自动构建为hugo 项目，相当于省略了本地执行 `hugo -D` 的过程。


旧的发布方式为：
1. obsidian中写作文章
2. 复制文件到 hugo 项目的 content/posts 文件夹
3. 然后执行 hugo -D 命令，生成静态文件
4. 再到public 文件夹下使用 git 将已生成的静态文件上传到 github。github page 作为博客展示。

现在我要发布一篇新博客时，只要在 obsidian 中打开 hugo博客的这个库，然后使用 quickadd 新建一篇博客，写上内容，然后把yaml 中的 `published`  字段值改为 `true` 即可（从草稿改为发布）。等待3分钟后 obsidian-git 插件自动同步到 github，博客就自动更新发布好了。

### 使用到的 obsidian 插件

#### image auto upload plugin

用于自动上传图片到图床。需要配合 picgo 使用。

#### quickadd

用于快速创建一篇新博客。

下面是我的设置：

1. 创建一个 `Template` 类型的quickadd 命令

![image.png](https://s2.loli.net/2023/03/11/HXaVj2uZneSE9l6.png)

2. 在根目录新建一个 `_Templates` 文件夹，并创建模板文件 `hugo博客模板`
![image.png](https://s2.loli.net/2023/03/11/wrHtPay62Dn8xGV.png)

4. 设置quickadd 命令：
![image.png](https://s2.loli.net/2023/03/11/Z9BDtVHJr2uaIyq.png)

#### obsidian-git

用于自动备份文件到 github。

插件设置修改如下：
![image.png](https://s2.loli.net/2023/03/11/cxTJiutPEfkHFW8.png)



### 参考

- 木木木木木： [Hugo With Obsidian](https://immmmm.com/hugo-with-obsidian/) 
- 木木木木木： [Hi , Cloudflare Pages](https://immmmm.com/hi-cloudflare/)
- [Hugo 博客写作最佳实践](https://blog.zhangyingwei.com/posts/2022m4d11h19m42s28/)
- [如何将域名托管到cloudflare](https://www.back2me.cn/skills/cloudflare.html)