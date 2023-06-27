---
title: 博客新增邮件订阅：TinyLetter
tags: [折腾]
date: 2023-06-27 20:24:37
UID: 20230627202437
draft: false
toc: false
feature: https://s2.loli.net/2023/06/27/yl4PXakHutnjI2E.png
---

事情开始于，有读者问邮件订阅。
<!--more-->

![image.png](https://s2.loli.net/2023/06/27/REPtuUZjTlHgMN3.png)

当我看到这条评论，心里是十分开心的，这说明有人想要邮件订阅我的博客，接收博客更新通知。哇！很感动好么！

好的，于是我开始找解决方案。


就我所知不太容易，没有现成的简易轮子可以用。从中文圈各大博客都没有邮件订阅就能看出来了（除了使用wordpress的博客站，有自带的邮件订阅功能）。

好在让我找到一篇：
[给静态博客添加newsletter的几种推荐方案](https://irithys.com/p/blog-newsletter/#tinyletter) 

最终选择了 [TinyLetter](https://app.tinyletter.com). 👆🏻文章中有教程，我就不再写啦。Tinyletter 对国内支持还算比较友好，这是我选择它的最大原因。

💫

我在文章底部增加了订阅表单，填写你的邮箱进行订阅吧~

或者点击 [这里](https://tinyletter.com/lillianwho) 进行订阅。（关于页面也增加了邮件订阅链接，不迷路）

有新文章时就能在邮件收到推送啦！

### 缺点

缺点就是我博客文章发布之后经常捉虫，进行修改，这样的修改邮件中是看不到的。

### 页面美化

原始的表单比较丑，于是用我磕磕绊绊的前端技术美化了一下。

`subscribe-form.html` 单独一个文件，使用时在 `single,html`模板中引入：
```html
<!-- 邮件订阅  -->
<link rel="stylesheet" href="/subscribe.css">
<div class="pagination">
  <div class="pagination__title">
    <span class="pagination__title-h">📮邮件订阅</span>
    <hr />
  </div>
  <p style="text-align: center;">想我每次发布新东西时都收到电子邮件吗？</p>
  <div class="sub_box">
    <form id="sub-form" action="https://tinyletter.com/lillianwho" method="post" target="popupwindow"
      onsubmit="window.open('https://tinyletter.com/lillianwho', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true">
      <p id="subscribe-email"><input type="email" class="sub-input input-email" name="email" id="tlemail"
          placeholder="输入你的邮箱地址..." required />
        <input type="hidden" value="1" name="embed" />
      </p>
      <p id="subscribe-submit"><input type="submit" value="订阅" class="sub-input input-submit" /></p>

    </form>
  </div>
</div>
```

css样式：`subscribe.css`
```css
/*
邮件订阅样式
*/
.sub_box{
    display: block;
    box-sizing: border-box;
    /* align-items: center; */
    
}

#sub-form{
    border:0;
    padding:3px;
    text-align:center;
    display: flex;
    /* align-items: flex-start; */
    justify-content: center;


    /* text-align: center; */
    /* align-content: center; */
}

p#subscribe-email, p#subscribe-submit{
    margin: 0;
    
    box-sizing: inherit;
    display: block;
}

p#subscribe-email{
    flex-grow: 1;
    max-width: 400px;
}



.sub-input {
    font-size: 16px;
    padding: 15px 23px 15px 23px;
    margin: 0px;
    border-radius: 0px;
    border-width: 1px;

    line-height: 1.3;
    box-shadow: none;
}

.input-email{
    margin: 0;
    width: 100%;
    
    color: #666;
    border: 1px solid #ccc;
    max-width: 100%;
    /* box-shadow: none; */
}

.input-submit{
    margin: 0px;
    margin-left: 10px;
    border-color:transparent;
    border-style: solid;
    background-color:#222;
    color: #fff;

    box-sizing: border-box;
    min-width: auto!important;
    
}
```

### 文章页效果

![image.png](https://s2.loli.net/2023/06/28/l3VyjOPAD1xKL2s.png)


