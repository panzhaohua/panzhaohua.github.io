---
title: svn瘦身
date: 2019-10-08 10:54:26
tags:
category: Svn基础
---
svn瘦身,因服务器空间不足，影响应用正常运行，所以尝试进行瘦身
1. 找到最新版本号
P800_IpvodUpdate 最大，所以瘦身从它开始；

```
svnlook youngest P800_IpvodUpdate
```

2. 创建备份库

```
svnadmin hotcopy  P800_IpvodUpdate 1008
```
命令完成后，因为空间太少，直接将1008移动
```
mv 1008/ /var/wwwtest/
```
3. 导出当前最新版本

```
svnadmin dump P800_IpvodUpdate -r 42 >42.tmp
```
4. 删除旧库

```
rm -rf P800_IpvodUpdate
```
5. 创建新的空版本库

```
svnadmin create P800_IpvodUpdate
```
6. 导入

```
svnadmin load P800_IpvodUpdate <42.tmp 
```
7. 检查是否成功

```
svn co svn://3woa.com/P800_IpvodUpdate
```

8. 删除备份

```
rm -rf  /var/wwwtest/1008
```



