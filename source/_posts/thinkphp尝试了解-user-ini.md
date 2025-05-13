---
title: thinkphp尝试了解.user.ini
date: 2025-05-13 14:44:14
tags: php
category: php
---
**thinkphp尝试了解.user.ini**
作为一个老运维部署php很多年了，没想到在部署最近一个thinkphp框架时遇到了问题，始终报403 access denied

No input file specified 这类错误，在phpf-pm错误， 项目的报错日志里面折腾了好久，然后又查看nginx日志，没找到原因，最后查找nginx errror日志，赫然发现提示 open\_basedir 限制，了解了下这个文件。 直接删除。坑。

ps:<https://www.php.net/manual/zh/configuration.file.per-user.php>

<https://blog.csdn.net/sinat_29193161/article/details/114009730>
