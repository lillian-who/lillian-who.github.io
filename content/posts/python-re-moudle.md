---
title: 'Python Re库'
date: 2022-08-31
tags: [技术/python]
draft: false
hideInList: false
feature: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg.cnpython.com%2Fmedia%2Findex%2Ft1.png&refer=http%3A%2F%2Fimg.cnpython.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1666101121&t=c8d943c088b543522c769b286a8a4d8d
isTop: false
---


**作用**： 提供对正则表达式的支持

<!--more-->

![](http://lillianwho.com/post-images/1661899153523.png)

## 用法
### 先引入库

```python
import re  # 引入正则库

```

### 创建模式对象进行匹配
```python
reg= "^131"
pat= re.compile(reg) #此处的参数是正则表达式
m = pat.search("13160785052") #此处参数是被校验的内容
print(m)
```


### 直接进行匹配

```python
reg= "^131"             # 正则表达式
str = "13160785052"     # 被验证的内容

m = re.search(reg,str)

print(m)
```

### 匹配所有符合条件的

```python
reg= "[A-Z]"             # 正则表达式，找大写字母
reg2= "[A-Z]+"             # 正则表达式，+表示前1个字符无限扩展，大写字母相连属于一次结果
str = "ABCccdHJKmiPM"     # 被验证的内容

m = re.findall(reg,str)     # 结果：['A', 'B', 'C', 'H', 'J', 'K', 'P', 'M']

m2 = re.findall(reg2,str)     # 结果：['ABC', 'HJK', 'PM']
print(m2)
```

### sub 替换

```python
str = r"abcdefgabcd" # 匹配对象
print(re.sub("a","A",str))    # 找到a 用A 替换
# 结果：AbcdefgAbcd
```


❗️建议在被匹配的字符串前加 `r`，可以保证字符不被转义

