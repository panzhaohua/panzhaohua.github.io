---
title: deliveryRobot的supervisor配置
date: 2019-10-15 13:05:45
tags: linux基础
category: supervisor基础
---
# deliveryRobot的supervisor配置
因deliveryRobot 需要新加一个计划任务，用于队列监听，所以开始了这次测试之旅。
- 配置supervisor

vim /etc/supervisord.d/deliveryRobot-listen.conf
```
[program:deliveryRobot-listen]
command=php /ubox/apps/deliveryRobot/artisan queue:listen  redis   --delay=3 --sleep=3 --tries=12            ; the program (relative uses PATH, can take args)
process_name=%(program_name)s_%(process_num)02d  ;
numprocs=5
priority=999                ; the relative start priority (default 999)
autostart=true              ; start at supervisord start (default: true)
autorestart=true            ; retstart at unexpected quit (default: true)
startsecs=10                ; number of secs prog must stay running (def. 10)
startretries=3  
user=www  
redirect_stderr=true
stdout_logfile=none
```
- 去除supervisor日志

因为我php设置问题，默认会有错误提示，导致supervisor日志很大，需要研究去掉日志。

```
redirect_stderr=true
stdout_logfile=none
```
- 重新加载配置文件

当成功创建配置文件后，需要刷新 Supervisor 的配置信息并使用如下命令启动进程:

```
sudo supervisorctl reread
sudo supervisorctl update
sudo supervisorctl start laravel-worker:*
```

---
PS：可以参考文档
https://xueyuanjun.com/post/19516.html
