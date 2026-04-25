---
title: "Nginx: Job for nginx.service failed because the control process exited 的解决办法"
slug: "nginx-job-for-nginx-service-failed-because-the-control-process-exited-的解决办法"
date: 2021-02-23T13:26:17
categories:
  - "cs"
tags:
  - "Nginx"
  - "notes"
---

最近在centOS 8.2手动部署nginx的时候发现了如下问题

启动Nginx后

``` shell
service nginx start
```

出现了报错

``` shell
Nginx: Job for nginx.service failed because the control process exited
```

首先检查一下nginx的配置文件语法是否正确，命令行输入

``` shell
nginx -t
```

若有语法错误会显示错误的位置，若语法正确仍然报错

可以尝试下面的方法解决

执行下列命令

``` shell
sudo fuser -k 80/tcp
sudo fuser -k 443/tcp
```

再执行

``` shell
sudo service nginx restart
```

解决！

发现这是因为此前服务器上预安装了Apache, 导致端口冲突，因此杀掉这两个进程就好了

参考网址：<https://stackoverflow.com/questions/35868976/nginx-job-for-nginx-service-failed-because-the-control-process-exited/51684856#51684856>
