---
title: centos6安装elasticsearch7.2、kibana7.2
date: 2019-11-07 17:04:00
tags: ELK基础
---
ktvplus安装elasticsearch、kibana

- 找到下载地址，直接wget 

wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.2.0-x86_64.rpm

wget https://artifacts.elastic.co/downloads/kibana/kibana-7.2.0-x86_64.rpm

- yum安装完毕，复制分词器ik、pinyin对应的jar包到plugins文件夹后启动服务，设置自启动；

```
yum install elasticsearch-7.2.0-x86_64.rpm -y
chkconfig elasticsearch on
service elasticsearch start


yum install kibana-7.2.0-x86_64.rpm -y
chkconfig kibana on
service kibana  start
```
kibana启动失败，日志报错 

```
 FATAL  Error: /lib64/libc.so.6: version `GLIBC_2.14' not found (required by /usr/share/kiba
na/node_modules/@elastic/nodegit/build/Release/nodegit.node)
```
解决办法：https://github.com/elastic/kibana/issues/40388
kibana只能127.0.0.1访问的问题
修改
```
vim /etc/kibana/kibana.yml 
#server.host: "localhost" 修改为 server.host: "0.0.0.0"
```
 

启动kibana，配置nginx代理；

```
upstream ktvplus_kibana {
    server 1.1.1.1:5601;
    }
server {
    listen 443 ssl;
    server_name ktvplus_elk.x.cn;
    ssl_certificate /etc/pki/tls/certs/xx/x.cn.crt;
    ssl_certificate_key /etc/pki/tls/private/x/x.cn.key;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

    # ACL
    # HSTS
    add_header Strict-Transport-Security "max-age=63072000; includeSubdomains; preload";
    location / {
        #auth_ldap "LDAP Login";
        #auth_ldap_servers ubox;
        autoindex on;
        #proxy_max_temp_file_size 0;
        fastcgi_buffer_size 4k;
        fastcgi_buffers 2048 512k;

        proxy_pass http://ktvplus_kibana;
        root html;
        index index.html index.htm;
    }
    error_page   500 502 503 504  /50x.html;

    location = /50x.html {
        root html;
    }

    access_log /x/logs/ktvplus/elk_access.log ubox;
    error_log /x/logs/ktvplus/elk_error.log;
}    
```



进行测试分词效果,使用kibana的Dev Tools 工具中的Console

elasticsearch自带分词器效果
```
GET _analyze?pretty=true
{
  "analyzer" : "standard",
  "text" : "我是一名java程序员"
}
```
使用ik_max_word分词
ik_max_word ：会将文本做最细粒度的拆分；尽可能多的拆分出词语
```
GET _analyze?pretty=true
{
  "analyzer" : "ik_max_word",
  "text" : "我是一名java程序员"
}
```
使用ik_smart分词
ik_smart：会做最粗粒度的拆分；已被分出的词语将不会再次被其它词语占有

```
GET _analyze?pretty=true
{
  "analyzer" : "ik_smart",
  "text" : "我是一名java程序员"
}
```

使用pinyin分词

```
GET _analyze?pretty=true
{
  "analyzer" : "pinyin",
  "text" : "我是一名java程序员"
}
```

---
PS:参考 https://blog.csdn.net/qq_28988969/article/details/79540620