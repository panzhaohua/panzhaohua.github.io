---
title: nacos1.4.1 升级到nacos2.0.3
date: 2026-01-30 10:34:04
tags: 运维
category: nacos
---
docker1.4.1升级到2.0.3
"1. 停止旧版本..."
docker-compose -f example/standalone-derby.yaml down

 "2. 备份数据..."
登录控制台 → 配置管理 → 配置列表 → 批量导出（如果有此功能）或逐个复制配置内容到本地文件。

 "3. 修改 docker-compose.yml 中的镜像版本...",手动指定版本为2.0.3
vim example/standalone-derby.yaml
image: nacos/nacos-server:2.0.3
 "4. 启动新版本..."
docker-compose -f example/standalone-derby.yaml up -d

 "5. 查看状态..."
docker-compose  -f example/standalone-derby.yaml ps

<https://github.com/nacos-group/nacos-docker.git>
升级到更新版本，需配置鉴权，先设置，预留

启动程序会提示您输入3个鉴权相关配置（Nacos从3.0.0版本开始默认启用控制台鉴权功能，因此如下3个鉴权相关配置必须填写）

Token Secret Key（JWT 密钥）

使用 OpenSSL 生成 32 字节随机字符串并 Base64 编码

`openssl rand -base64 32`
Euy6WnD9styBO6YXTxtn5EsxnAbwe+OD96YrbaUhIR8=
  Server Identity Key & Value
这两个是自定义字符串，用于集群节点间的身份识别，集群内所有节点必须保持一致。
生成随机字符串作为 key 和 value（可以相同，也可以不同）
`openssl rand -base64 12  # 作为 identity.key`
2aRxCqyDfFVUht1o
`openssl rand -base64 16  # 作为 identity.value`
yDHnOFrWM70/sNtxOZzciA==
JWT Token 密钥（必须是 Base64 编码，原始长度≥32字符）


nacos.core.auth.plugin.nacos.token.secret.key=
VGhpc0lzTXlDdXN0b21TZWNyZXRLZXkwMTIzNDU2Nzg5MA==
服务端身份识别（集群节点间必须一致）
nacos.core.auth.server.identity.key=myIdentityKey
nacos.core.auth.server.identity.value=myIdentityValue123
