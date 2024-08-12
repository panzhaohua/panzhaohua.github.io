---
title: centos6的open ssh版本过低无法迁移jenkins
date: 2024-08-12 14:20:12
tags: jenkins
category: jenkins
---
# centos6的open ssh版本过低无法迁移jenkins

由<https://groups.google.com/g/jenkinsci-users/c/689xrO2cAMo得>
jenkins里面的Publish Over SSH插件 jsch(the SSH library used) not support ssh-rsa；所以无法支持centos6
centos6无法支持ssh-ed25519等；
jenkins报错
`[ERROR: Exception when publishing, exception message \[Failed to connect and initialize SSH connection. Message: \[Failed to connect session for config \[mbss02]. Message \[Algorithm negotiation fail: algorithmName="server\_host\_key" jschProposal="ssh-ed25519,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,rsa-sha2-512,rsa-sha2-256" serverProposal="ssh-rsa,ssh-dss"]`
解决方法：
<https://issues.jenkins.io/browse/JENKINS-71273>
直接在 vim   /usr/lib/systemd/system/jenkins.service加上环境变量
`Environment="JAVA\_OPTS=-Djava.awt.headless=true -Djsch.client\_pubkey='ssh-ed25519,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,rsa-sha2-512,rsa-sha2-256,ssh-rsa'   -Djsch.server\_host\_key='ssh-ed25519,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,rsa-sha2-512,rsa-sha2-256,ssh-rsa'"`
再执行
`systemctl daemon-reload`

***

jenkins为解决Publish Over SSH支持centos6的ss-rsa算法，加了环境变量，迁移时也带上，不然发布到mbss线上会失败；
\-Djsch.client\_pubkey='ssh-ed25519,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,rsa-sha2-512,rsa-sha2-256,ssh-rsa'   -Djsch.server\_host\_key='ssh-ed25519,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,rsa-sha2-512,rsa-sha2-256,ssh-rsa'

