---
title: 'Python 爬虫'
date: 2022-08-31
tags: [技术/python]
draft: false
hideInList: false
feature: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg.cnpython.com%2Fmedia%2Findex%2Ft1.png&refer=http%3A%2F%2Fimg.cnpython.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1666101121&t=c8d943c088b543522c769b286a8a4d8d
isTop: false
---
用Python 爬取网页数据。附学习资料
<!--more-->

## 爬虫的定义

网络爬虫，就是按照一定的**规则**，**自动抓取**互联网信息的自动程序或脚本。

## 爬虫的本质

**模拟浏览器**打开网页，获取网页中我们需要的信息。

## 学习资料

[Python入门+Python爬虫+Python数据分析5天项目实操](https://www.bilibili.com/video/BV12E411A7ZQ?p=15&vd_source=ebb94d57c4e84cc0314c73e881f25a9c)

P.S. Python基础语法已经学过的，可以跳过P15之前。从P15-P18是Python爬虫的教程。

以爬取豆瓣电影TOP250的基本信息为例。

目标网页：https://movie.douban.com/top250

## 流程

### 1.准备工作
浏览目标网页，分析网页元素。

每个爬虫任务，都需要先分析目标网页。

爬虫爬到的就是网页源代码。

#### 分析URL

![](https://s2.loli.net/2022/09/21/KnwqbexJzutFE9B.png)

URL分析结果：
1. 页面包括250条电影信息，每页25条，共分为10页。
2. 每页URL的不同之处在于后的数值 `?start=(页数-1)*25`

#### 分析页面元素

![](https://s2.loli.net/2022/09/21/Qh6lIBGespLzAjv.png)

#### 找到请求头

![](https://s2.loli.net/2022/09/21/v7g41AXLJSyPZiw.png)



### 2.获取数据

利用urllib模块 获取网页html

```python
# 得到指定一个URL的网页信息
def askUrl(url):
    # 模拟浏览器头部信息
    head = {
        # 用户代理，告诉豆瓣服务器我们是什么浏览器
        "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.1 Safari/605.1.15"
    }
    request = urllib.request.Request(url,headers=head)   #构建请求
    try:
        response = urllib.request.urlopen(request)  # 发送请求，也就是模拟打开url
        html = response.read().decode("utf-8")                  # 从返回中读取网页内容
    except urllib.error.URLError as e:  # 捕捉错误
        if hasattr(e,"code"):
            print(e.code)
        if hasattr(e,"reason"):
            print(e.reason)

    #print(html)
    return html
```


### 3.解析内容

python BeautifulSoup 模块  ：解析html内容

Re 库，正则提取
{{<link "python-re-moudle">}}

#### 提取豆瓣电影数据的正则
```python
# ------提取豆瓣数据的正则
# 影片的链接
findLink = re.compile(r'<a href="(.*?)">')
# 影片图片的链接
findImgSrc = re.compile(r'<img.*src="(.*?)"',re.S)  # re.S 让换行符包含在字符中
# 影片片名
findTitle = re.compile(r'<span class="title">(.*?)</span>')
# 影片的评分
findRating = re.compile(r'<span class="rating_num" property="v:average">(.*?)</span>')
# 评分人数
findJudge = re.compile(r'<span>(\d*)人评价</span>')
# 介绍
findInq = re.compile(r'<span class="inq">(.*)</span>')
```

#### 提取电影数据
```python
datalist = []  # 所有电影数据
for item in t_list:
    
    # print(item.get_text())
    data =[]    # 保存一部电影的所有信息
    item = str(item)    #转为字符串，以供正则匹配
    # print(item)
    link = re.findall(findLink,item)[0] # 找到匹配到的链接的第1个
    imgSrc = re.findall(findImgSrc,item)[0]
    
    titles = re.findall(findTitle,item)
    if(len(titles)>1):  #如果有外文名
        ctitle = titles[0]
        otitle = titles[1].replace("/","")  #去掉无关符号
    else:
        ctitle = titles[0]
        otitle = ""         # 如果没有外文名，则留空字符串。因为要保存列表，列数要一致

    rating = re.findall(findRating,item)[0]
    judge = re.findall(findJudge,item)[0]
    inq = re.findall(findInq,item)[0]

    data.append(link)
    data.append(imgSrc)
    data.append(ctitle)
    data.append(otitle)
    data.append(rating)
    data.append(judge)
    data.append(inq)

    datalist.append(data)   # 把处理好的一部电影的信息放入datalist
# 打印查看结果
print(datalist)
```

### 4.保存数据

保存到Excel：

{{<link "python-xlwt-moudle">}}

## 实例完整代码

```python
#!/usr/bin/python3
# -*- coding: UTF-8 -*-
# 网页爬虫。

# 目标：爬取豆瓣电影Top250的信息。
# 目标网页：https://movie.douban.com/top250

# 1. 分析网页
# URL分析结果：页面包括250条电影信息，每页25条，共分为10页。每页URL的不同之处在于后的数值 ?star=(页数-1)*25
# 页面元素分析


#网页解析，截取数据
import re   #正则表达式
import urllib.request,urllib.error
from bs4 import BeautifulSoup      #发送请求，获取网页数据
import xlwt     #进行excel 操作
# import sqlite3  #SQLite 数据库操作

#主程序，执行入口
def main():
    baseurl="https://movie.douban.com/top250"
    savepath="豆瓣电影Top250.xls"
    # 1.爬取所有网页并返回解析过的数据
    datalist = getData(baseurl)
    # 3.保存数据
    saveData(datalist,savepath)



# ------提取豆瓣数据的正则
# 影片的链接
findLink = re.compile(r'<a href="(.*?)">')
# 影片图片的链接
findImgSrc = re.compile(r'<img.*src="(.*?)"',re.S)  # re.S 让换行符包含在字符中
# 影片片名
findTitle = re.compile(r'<span class="title">(.*?)</span>')
# 影片的评分
findRating = re.compile(r'<span class="rating_num" property="v:average">(.*?)</span>')
# 评分人数
findJudge = re.compile(r'<span>(\d*)人评价</span>')
# 介绍
findInq = re.compile(r'<span class="inq">(.*)</span>')

# 爬取网页并解析数据
def getData(baseurl):
    datalist = []
    for i in range(0,10):   #10个页面
        url = baseurl + "?start=" +str(i * 25)
        html = askUrl(url)

        # 2.解析数据（逐一解析）
        soup = BeautifulSoup(html,"html.parser")    # 用 bs的html解析器
        for item in soup.find_all('div',class_="item"):  # 找 class属性="item"的div
            data =[]    # 保存一部电影的所有信息
            item = str(item)    #转为字符串，以供正则匹配
            # print(item)
            link = re.findall(findLink,item)[0] # 找到匹配到的链接的第1个
            imgSrc = re.findall(findImgSrc,item)[0]
            titles = re.findall(findTitle,item)
            if(len(titles)>1):  #如果有外文名
                ctitle = titles[0]
                otitle = titles[1].replace("/","")  #去掉无关符号
            else:
                ctitle = titles[0]
                otitle = ""         # 如果没有外文名，则留空字符串。因为要保存列表，列数要一致

            rating = re.findall(findRating,item)[0]
            judge = re.findall(findJudge,item)[0]
            inqs = re.findall(findInq,item)
            if(len(inqs)>0):
                inq = inqs[0]
            else:
                inq = ""

            data.append(link)
            data.append(imgSrc)
            data.append(ctitle)
            data.append(otitle)
            data.append(rating)
            data.append(judge)
            data.append(inq)

            datalist.append(data)
    
    # 返回解析过的数据
    return datalist

# 保存数据到Excel
def saveData(datalist,savepath):
    workbook = xlwt.Workbook(encoding="utf-8")  #创建wookbook 对象
    worksheet = workbook.add_sheet("豆瓣电影TOP250",cell_overwrite_ok=True)    # 创建工作区
    # cell_overwrite_ok=True 允许覆盖以前的内容
    coltitle = ("电影详情链接","图片链接","影片中文名","影片外文名","评分","评价数","简介")

    # 写入列名
    for i in range(0,len(coltitle)):
        worksheet.write(0,i,coltitle[i])
    
    # 写入数据
    for row in range(0,len(datalist)):  # 总行数为数据条数
        data = datalist[row]
        for col in range(0,len(coltitle)):   # 7列
            # 从第 (1,0)开始写
            worksheet.write(row+1,col, data[col])

    workbook.save(savepath)

    return

# 得到指定一个URL的网页信息
def askUrl(url):
    # 模拟浏览器头部信息
    head = {
        # 用户代理，告诉豆瓣服务器我们是什么浏览器
        "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.1 Safari/605.1.15"
    }
    request = urllib.request.Request(url,headers=head)   #构建请求
    try:
        response = urllib.request.urlopen(request)  # 发送请求，也就是模拟打开url
        html = response.read().decode("utf-8")                  # 从返回中读取网页内容
    except urllib.error.URLError as e:  # 捕捉错误
        if hasattr(e,"code"):
            print(e.code)
        if hasattr(e,"reason"):
            print(e.reason)

    #print(html)
    return html


# 此处是保证程序入口唯一，保证执行流程可控
if __name__ == "__main__":
    # 调用函数
    main()


```

### 执行结果

运行后得到一个Excel，检查一下数据无误后即可。我第一次爬的时候第一页数据一直重复，没有读到后面页面的数据，检查源代码才发现url后面的参数名拼错了。

![](https://s2.loli.net/2022/09/19/yvYudfBCIDHN6x1.png)