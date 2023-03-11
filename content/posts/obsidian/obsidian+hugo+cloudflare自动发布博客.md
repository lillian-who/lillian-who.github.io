---
title: obsidian+hugo+cloudflare自动发布博客
tags: [折腾,博客]
date: 2023-03-11 17:20:56
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


### 参考

- 木木木木木： [Hugo With Obsidian](https://immmmm.com/hugo-with-obsidian/) 
- 木木木木木： [Hi , Cloudflare Pages](https://immmmm.com/hi-cloudflare/)
- [Hugo 博客写作最佳实践](https://blog.zhangyingwei.com/posts/2022m4d11h19m42s28/)
- [如何将域名托管到cloudflare](https://www.back2me.cn/skills/cloudflare.html)