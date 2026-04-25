---
title: "PicGo图床+GitHub链接配置方法"
slug: "picgo图床github链接配置方法"
date: 2021-02-23T16:03:12
categories:
  - "cs"
tags:
  - "markdown"
  - "notes"
  - "PicGo"
  - "typora"
  - "图床"
---

最近已经相当习惯于用typora写东西，清晰简洁，也可以直接复制到wordpress发布，各大主流平台也基本都支持markdown的格式。但typora唯一的不方便之处就是图片的链接就十分麻烦，首先是电脑上截屏的图片虽说可以直接粘到typora里，但是截屏的图片是保存在剪贴板里的，链接一段时间后就会失效。其次是直接把md复制到博客中的话图片还要另外上传到服务器中，再重新设置链接，就让人十分烦恼。

今天发现了typora还自带配置图床功能（越发感觉typora的优秀了），于是打算配置一个图床。图床就是将图片上传到服务器上，这样博客和本地都可以通过这个链接访问到图片，不需要麻烦地粘链接啦（当然这需要有网）

## 下载PicGo

PicGo是typora支持的一个图床软件，在typora上可以直接通过PicGo上传图片并自动生成链接。

去GitHub下载PicGo

<https://github.com/Molunerfinn/PicGo/releases>

windows下载exe文件 macOS下载dmg文件

安装

## 创建GitHub仓库

1.  在用户下拉面板 – Your repositories – New

    <img src="/img/external/gitee.com/jackiehu_2020/picture/raw/master/img/pic1.png" decoding="async" alt="pic1" />

2.  获取token

    在 Settings – Developer settings – Personal access tokens

    <img src="/img/external/gitee.com/jackiehu_2020/picture/raw/master/img/pic2.png" decoding="async" alt="img" />

    输入Note，勾选repo，再点击下方的 generate token

    复制token，保存下来（它只会出现一次）

## 配置PicGo

点击图床设置-Github图床

仓库名是username/你刚刚设置的名字

分支刚刚生成的默认分支是main，也可以自己新建分支

Token就是刚刚生成的token

存储路径img/就好

**确定！** 完成！

## 在typora中使用PicGo

偏好设置中

<img src="/img/external/gitee.com/jackiehu_2020/picture/raw/master/img/image-20210223155904428.png" decoding="async" alt="image-20210223155904428" />

将上传服务设为PicGo(app)，路径写刚刚安装的exe的路径就好啦😜

以后打算就用 wordpress+typora+PicGo的写作模式啦
