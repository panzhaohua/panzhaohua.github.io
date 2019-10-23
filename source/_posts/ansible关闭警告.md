---
title: ansible关闭警告
date: 2019-10-16 15:31:52
tags: linux基础
category: ansible基础
---
# ansible关闭警告
最近升级了下使用的ansible,warn信息就层出不从，每次运行都有很多提示。今天比较闲，于是计划解决这个问题。
- DEPRECATION警告

```
[DEPRECATION WARNING]: Distribution Ubuntu 16.04 on host 172.17.56.20 should 
use /usr/bin/python3, but is using /usr/bin/python for backward compatibility 
with prior Ansible releases. A future Ansible release will default to using the
 discovered platform python for this host. See https://docs.ansible.com/ansible
/2.8/reference_appendices/interpreter_discovery.html for more information. This
 feature will be removed in version 2.12. Deprecation warnings can be disabled 
by setting deprecation_warnings=False in ansible.cfg.
```
选择在ansible.cfg设置 deprecation_warnings=False 
- Invalid characters 警告

```
 [WARNING]: Invalid characters were found in group names but not replaced, use
-vvvv to see details
```
总提示我组名有不符合的字符，网上搜索了下，组名不能包含 字母 数字 下划线以外的符号，且不能以数字开头。修改之，同时修改使用的 jenkins、计划任务，免得以后任务报错。保存。
不再报警。

```
[a.b]
172.17.56.16
```
修改为

```
[a_b]
172.17.56.16
```
