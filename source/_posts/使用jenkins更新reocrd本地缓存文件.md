---
title: 使用jenkins更新reocrd本地缓存文件
date: 2019-10-23 12:02:44
tags: linux基础
category: 自动运维
---
#### 使用ansible实现录音文件更新
##### 脚本部分
- ansbile工具的shell、command、script、raw模块的区别和使用场景

https://blog.51cto.com/lansgg/1745009

- 使用shell模块，使用的远程主机的shell脚本，所以需先把脚本copy过去

```
ansible record -m copy -a "src=/ubox/scripts/record/record-wget.bash dest=/root/ mode=500"
```

- 先测试下脚本（在此之前，我已经测试过其他脚本）

record-1 
```
bash -x record-wget.bash yb00083.aac
```
3woa-119

```
ansible 172.16.57.135 -m shell  -a "/root/record-wget.bash yb00083.aac"
```
##### 其他部分为jenkins图形化配置
![image](/2019/10/23/使用jenkins更新reocrd本地缓存文件/record/12.png)
![image](/2019/10/23/使用jenkins更新reocrd本地缓存文件/record/3.png)
---
PS:
简单测试脚本  test.bash

```
echo 'date'
echo ${1}
```
脚本执行：
record-1: 
``` 
bash -x test.bash 123
```

3woa: 
``` 
ansible 172.16.57.135 -m shell  -a "/tmp/test.bash aa"
```