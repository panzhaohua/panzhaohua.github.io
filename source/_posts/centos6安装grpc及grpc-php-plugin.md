---
title: centos6安装grpc及grpc_php_plugin
date: 2020-03-16 11:34:43
tags: grpc
category: grpc基础
---
centos6安装grpc及grpc_php_plugin

参考文献 
https://www.cnblogs.com/chenqionghe/p/12394845.html
https://www.luyouli.com/?p=52
https://copyfuture.com/blogs-details/2019070713183245608cbpk2s1yl1lc5

发现centos6 安装 grpc前需要做的事情就是升级gcc到4.8以上，推荐scl源升级


```
yum -y install centos-release-scl
yum -y install devtoolset-8-gcc devtoolset-8-gcc-c++ devtoolset-8-binutils
scl enable devtoolset-8 bash
```


然后再安装其他编译工具。

```
yum install automake autoconf libtool -y
```

然后坑点来了，网上说的 make grpc_php_plugin 可以这样操作。


```
git clone -b $(curl -L https://grpc.io/release) https://github.com/grpc/grpc
cd grpc
git submodule update --init
make && sudo make install

# 生成的插件路径
ll ./bins/opt/

# 复制到bin目录
cp -r ./bins/opt/* /usr/local/bin/
```
我始终不能成功，总是提示缺少文件，最后发现是因为我没有先编译protoc，是直接下载二进制文件解压缩的。

最后先编译了protoc再编译 grpc_php_plugin ，一次搞定。
PS:
nodejs glibc都可以不更新，推荐不要动。稳定第一。



