---
title: minikube k8s 安装指引
date: 2020-07-14 11:43:58
tags: K8S
category: K8S
---
#### minikube k8s 安装
1. 安装docker 
```
yum install -y docker
```
2. 安装kubectl minikube helm

```
https://kubernetes.io/docs/tasks/tools/install-minikube/?ref=hackernoon.com
https://kubernetes.io/docs/tasks/tools/install-kubectl/?ref=hackernoon.com
https://helm.sh/docs/intro/install/?ref=hackernoon.com
```
下载到本地保存好，然后拷贝到虚拟机去； 

```
mv  * /usr/local/bin/
```
3. 创建集群

```
minikube start --driver=none
```
提示 X Sorry, Kubernetes 1.18.3 requires conntrack to be installed in root's path ，安装conntrack 
```
yum install conntrack -y
```
再跑，提示ubox 不能被解析，加入 /etc/hosts 文件

```
vi /etc/hosts
127.0.0.1  ubox
```
关掉防火墙，设置服务自动启动
```
systemctl enable kubelet.service
systemctl start  kubelet.service
systemctl stop firewalld
systemctl disabel firewalld
```
再遇到报错

```
/proc/sys/net/bridge/bridge-nf-call-iptables contents are not set to 1
```
解决方案

```
echo 1 >/proc/sys/net/bridge/bridge-nf-call-iptables
```
经典网络问题因公司有代理，所以未遇到，但也标记解决办法

```
minikube start --vm-driver=none --image-repository=registry.cn-hangzhou.aliyuncs.com/google_containers
```
再遇到报错

```
Failed to list *v1.Node: Get https://control-plane.minikube.internal:8443/api/v1/nodes?limit=500&resourceVersion=0: dial tcp 10.0.2.15:8443: connect: connection refused
Failed to list *v1.StorageClass:
```
解决办法： 关闭selinux 

```
临时： setenforce 0
永久：
vi /etc/sysconfig/selinux
SELINUX=disabled
```
再运行minikube status

```
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
```
收工！！！




---
PS:
系统基于centos7

安装vim  lrzsz和bash-completion 

```
yum install -y  lrzsz vim bash-completion
```
https://kubernetes.io/zh/docs/tasks/tools/install-minikube/

卸载minikube

```
minikube delete
```
运行以下命令查看 Redis 主节点 Pod 中的日志：
```
kubectl logs -f POD-NAME
```
查看信息

```
kubectl describe pods  POD-NAME
```


