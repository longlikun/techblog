---
author: longlikun
title : 怎么在wsl中使用hugo
date : 2024-03-13T15:21:01+08:00
description: 怎么在wsl中使用hugo
draft: false
math: true
categories:
    - Test
    - 随笔

tags :
   - github

---

# 前言

在windows 系统上面使用程序类相关的应用，我喜欢在wsl中使用，因为以前在windows经常会遇到环境变量路径这种那种的错误,这次在wsl2中安装使用hugo,使用hugo的时候遇到的几个问题，记录下来，以备后面查看。

### 1 使用存储库包安装hugo
按照hugo官网的说明，https://gohugo.io/installation/linux/ ，使用存储库安装hugo是很简单的,在linux上面，我使用系统版本是ubuntu20， 只要一条命令就能解决。

```bash
sudo apt update && sudo apt install hugo
```
这样安装的版本只有0.68，到目前为止2024年3月，最新的版本是0.123.8，所以这样按照的版本不符合要求。

### 使用snap安装
根据官网安装说明，linux推荐使用sanp安装，Snap是一款适用于 Linux 的免费开源包管理器。snap 包适用于大多数发行版，安装简单并且会自动更新。这样对于我的服务器上的是可以的

```shell
    sudo snap install hugo
```
但是在我的win11中，使用的wsl2，snapd 是unavaiable，找了很多解决办法，但是涉及到很多其他的东西，貌似都有点麻烦。所以放弃这个安装方法。

### 使用github源安装

在查看hugo的github库的下载包，https://github.com/gohugoio/hugo/releases/，可以看到有几个deb包，我们可以下载下来使用dpkg安装，首先下载deb包，
这里我使用wget下载

```bash
wget https://github.com/gohugoio/hugo/releases/download/v0.123.8/hugo_0.123.8_linux-amd64.deb
```
下载完成后，移动到你的文件夹，然后进入到文件夹安装
```bash
mv hugo_0.123.8_linux-amd64.deb ～/you-document/hugo/
cd ～/you-document/hugo/
```
安装hugo

```bash
dpkg -i hugo_0.123.8_linux-amd64.deb
```
安装完成后，查看hugo版本

```bash
hugo version
```
版本为0.123.8，这样我们可以使用了，但是一般来说我们使用hugo需要安装扩展版本，因为很多模板都是需要使用扩展版本的，但是这样安装的不是extend版本



### 从github api中下载

首先在gohugoio 的gitphub api库中查询你需要的版本，然后下载

https://api.github.com/repos/gohugoio/hugo/releases/latest


使用wegt 下载
```bash
wget https://github.com/gohugoio/hugo/releases/download/v0.123.8/hugo_extended_0.123.8_linux-amd64.deb
```
和上面一样，下载完成后，使用dpkg 安装

安装完成后，再查看版本，已经是extended 版本了

```bash
hugo v0.123.8-5fed9c591b694f314e5939548e11cc3dcb79a79c+extended
```

下面可以安装hugo 的快速使用https://gohugo.io/getting-started/quick-start/，安装模板和写文章了

参考 


<a href="[超链接地址](https://gohugo.io/)" title="超链接title">hugo官网</a>


<a href="[超链接地址](https://computingforgeeks.com/how-to-install-hugo-on-ubuntu-debian/)" title="怎么在ubuntu上安装hugo">怎么在ubuntu上安装hugo</a>

