---
title: github学习一
date: 2019-09-27 16:57:14
tags:
category: 爬虫基础
---
学习的几个github库
1. [daacheng/PythonBasic/](https://github.com/daacheng/PythonBasic)

http的所有基本请求方法网站： http://httpbin.org
```
import requests
r = requests.get(url, headers=heasers,cookies=cookies, timeout=0.001,proxies=proxies)
```
#### css选择器(soup.seclect())
1. 通过标签名soup.select('title')
2. 通过类名查找 soup.select('.sister')
3. 通过id名查找soup.select('#link1')
4. 组合查找 soup.select('p #link1')
5. 属性查找 soup.select('a[href="http://examle.com/elsie"]')
#### xpath解析
F12  右键copy xpath

---
selenium模拟鼠标操作

目前scarpy除了下载图片，还没发现其他用处

