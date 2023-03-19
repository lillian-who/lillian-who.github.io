---
title: obsidian复习插件-flashcards
date: 2022-10-20
tags: [Obsidian,Obsidian插件]
toc: true
draft: false
hideInList: false
isTop: false
---

最近要考试，整理的笔记有点多，背的时候觉得不管是对着电脑背还是打印出来背，效果都差强人意，忽然想到借助一点工具。 既然我题都整理好了，如果能利用 Obsidian 的复习插件进行背诵，岂不是更好？

奈何之前的间隔复习插件（obsidian-spaced-repetition）只识别一个标签，对整个笔记进行复习，不太友好。闪卡模式要单独整理笔记...... 总之在 Obsidian 里面复习效果一般。

于是找到了新的插件，flashcards，运用 Obsidian 写笔记的便利，批量生产卡片到 Anki 中。在Ob里写卡片，在 Anki 里进行复习，各自完成专业的事，完美！

<!--more-->

## 插件介绍

### 插件作用

连接 anki ，在 Obsidian 里面编辑内容，通过命令创建卡片，自动同步到Anki里。


### 安装

从插件市场安装。

详细信息请访问 github 主页： [reuseman/flashcards-obsidian](https://github.com/reuseman/flashcards-obsidian)

使用教程： https://github.com/reuseman/flashcards-obsidian/wiki

## 使用方法

### 1、安装插件并连接anki

1. 在 Obsidian 里安装 flashcards 插件，并启用
2. 安装 Anki，并打开
	-   工具 > 附加组件 -> 获取附加组件...
	-   粘贴代码 **2055492159** > OK
3. 返回 Obsidian ，打开 flashcards 插件的设置项， 点击 `give permission` 后面的按钮，获取 Anki 权限
4. 点击 `test anki` 测试连接，检查权限，提示 `anki work` 表示连接成功

![](https://s2.loli.net/2022/10/20/yXR93ZizmsHIpdF.png)


### 2、写抽认卡

#### `cards` 标签

只要给小标题加上 `#cards` 标签，即可，该标签可以在设置项里指定。只有被指定的标签才会被 flashcards 插件识别为抽认卡

```md
## 这是一个问题 #cards 
这是一个答案

```

在设置项里，可以修改识别的标签。

![](https://s2.loli.net/2022/10/20/AVTeEa1xwGqRpJO.png)


#### 内联样式

语法是两个英文冒号

```md
这是第二个问题:: 这是第二问题的答案
```

#### 指定牌组

牌组是 Anki 中的概念。

要指定牌组，可以设置一个默认牌组，或者在每一个笔记里指定一个牌组。

![](https://s2.loli.net/2022/10/20/hzAUmaeRxnZXcB5.png)


笔记里指定牌组名称，使用 yaml 语法：

```md
---
cards-deck: 管理数量方法
---

```




### 3、生成卡片到 Anki 中

在 Obsidian 中 `ctrl/command + P` 打开命令面板，运行命令 `Flashcards: Generate for the current file` 。该命令的作用是从当前文件生成卡片到 Anki 中

![](https://s2.loli.net/2022/10/20/SjlqtJmTRZ9vye5.png)


#### 复习

打开 Anki ，在 Anki 中复习相应牌组即可。