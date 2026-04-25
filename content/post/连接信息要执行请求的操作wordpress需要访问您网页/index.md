---
title: "连接信息：要执行请求的操作，WordPress需要访问您网页服务器的权限问题"
slug: "连接信息要执行请求的操作wordpress需要访问您网页"
date: 2021-02-23T15:19:23
categories:
  - "cs"
tags:
  - "notes"
  - "权限问题"
  - "连接信息"
---

安装好wordpress后，在进行更新和安装插件时，遇到了 **“要执行请求的操作，WordPress需要访问您网页服务器的权限。 请输入您的FTP登录凭据以继续。 如果您忘记了您的登录凭据（如用户名、密码），请联系您的网站托管商。”** 这个问题， <img src="/img/external/gitee.com/jackiehu_2020/picture/raw/master/img/20150829195621_52974.png" decoding="async" alt="【已解决！】要执行请求的操作，WordPress需要访问您网页服务器的权限问题" />

即使输入密码也会显示错误，百度发现这是由于服务器端的权限设置问题，由于我是用的独立服务器，因此需要的是修改网站所在目录属性

``` shell
chmod -R 777 /data/www/wordpress
```

其中 /data/www/wordpress 需要改为你自己的网站路径

再执行

``` shell
chown -R www /data/www/wordpress
```

www为nginx/apache的user name, 可进入conf文件获知

/data/www/wordpress 同样的为网站路径

其实出现这个的问题就是Apache/Nginx的执行身份非文件属主身份。

更多的可参考：

<https://seofangfa.com/wordpress-study/ftp.html>
