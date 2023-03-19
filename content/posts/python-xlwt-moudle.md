---
title: 'python xlwt模块'
date: 2022-08-31
tags: [技术/python]
draft: false
hideInList: false
feature: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg.cnpython.com%2Fmedia%2Findex%2Ft1.png&refer=http%3A%2F%2Fimg.cnpython.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1666101121&t=c8d943c088b543522c769b286a8a4d8d
isTop: false
---

**作用**：用于操作Excel

<!--more-->


## 代码示例

```python
#!/usr/bin/python3
# -*- coding: UTF-8 -*-
# 保存数据到Excel

import xlwt

workbook = xlwt.Workbook(encoding="utf-8")  #创建workbook 对象
worksheet = workbook.add_sheet("sheet1")    # 创建工作区

# 写入数据

worksheet.write(0,0,"hello")    # 第一个参数是行，第二个参数是列。第三个参数是内容
workbook.save('test.xls')

### 写个九九乘法表

```python
import xlwt

workbook = xlwt.Workbook(encoding="utf-8")  #创建wookbook 对象
worksheet = workbook.add_sheet("九九乘法表")    # 创建工作区

# 写个九九乘法表

for row in range(0,9):  # 行

    for col in range(0,row+1):   # 列
      
        worksheet.write(row,col,"%d * %d = %d"%(col+1,row+1,(col+1)*(row+1)))

workbook.save('test2.xls')