---
title: scrapy中xpath使用小计
category: Python基础
date: 2019-9-2
---
scrapy下写的一个爬虫方法，是用来爬取html页面的title标签内容和class='note'的div标签下的内容
```
def next(self,response):
    title = response.xpath("/html/head/title/text()").extract()
    note = response.xpath("//div[@class='note']/text()").extract()
    print(title)
    print(note)
```
1. xpath是什么

Xpath是一门在XML文档中查找信息的语言，可以对XML文档中的元素和属性使用路径表达式进行导航，Xpath包含一个标准函数库。

2. xpath常用标签
```
　　/ ------提取某个标签下的所有内容
　　text() ------- 提取标签所包含的文本内容
　　@ ---------- 提取标签属性的信息
　　// ---------- 寻找所有的标签
　　[@属性=值] ------ 定位标签
```
3. 使用举例

```
　　/html -----代表提取html标签内的所有内容
　　/html/head/title -----代表提取title下面的所有信息
　　//li ------ 代表提取所有的li标签
　　//li[@class='hidden-xs'] -------- 直接定位到满足条件的标签
　　//li[@class='hidden-xs']/a/@heef ---------- 提取到class = hidden-cs的li标签下面的a标签的href的值
```






