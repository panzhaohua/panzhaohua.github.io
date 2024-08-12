---
title: 用powershell给ad账户续期6个月的需求
date: 2023-12-12 14:20:12
tags: powershell
category: powershell
---
# 用powershell给ad账户续期6个月的需求

以前每次用命令行来续期，感觉操作的时候，需要手动去掉前后空格，每次去掉用户名部分，所以整合成一个脚本，每次只需要复制用户民即可，还可以自动去掉空格。
需要管理员账号执行脚本
-----------

    for (;;)  
    {   
        $ID = Read-Host "请输入你要续期的用户名"
        $ID = $ID.Trim()
        echo "你要续期的用户名是:"$ID 
        Set-ADAccountExpiration  -TimeSpan 190.0:0  -Identity  $ID
        echo "请确认下续期用户是否已续期成功"
        net user $ID 
    }

### 追加提示，用Kimi等gpt可以修改为更好的脚本；
